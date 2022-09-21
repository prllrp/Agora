<template>
  <div class="root">
    <div class="banner">
      <Banner />
    </div>
    <div class="main">
      <Explorer :rooms = 'rooms' @add-room = 'createRoom' @join-room = 'setChannel' />
      <Chat @send-message = 'sendMessage' :messages = 'messages' @block = 'blockUser' />
      <Info :channel = 'this.channel' :nodePeers="this.peers" :nodeStatus='this.nodeStatus' :nodeId="this.me" :alias = 'alias'
      @change-alias = 'setAlias'></Info>
    </div>
  </div>
</template>

<script>
import Explorer from '~/components/Explorer.vue';
import Chat from '~/components/Chat.vue';
import Info from '~/components/Info.vue';
import Banner from '../components/Banner.vue';
import { onMounted } from 'vue';
export default {
    name: "IndexPage",
    components: { Explorer, Chat, Info, Banner },
    data(){
      return {
      defaultChannel:{
        id: 99999,
        name: 'Agora',
        description: 'General chat',
      },
      messages: [],
      rooms: [],
      alias: 'Anonymous',
      channel: {
        id: 99999,
        name: 'Agora',
        description: 'General chat'}, 
      peers: [],
      peerCount: 0,
      nodeStatus: 'Offline',
      me: '',
      blockList: [],
    }
    },
    methods: {
      blockUser(address){
        this.blockList.push(address);
        console.log(this.blockList)
      },
      setAlias(alias){
        this.alias = alias.alias;
      },
      async checkAlive() {
        this.peers = await this.node.swarm.peers()
        let now = new Date().getTime();
        if (now - this.lastAlive >= 35000) {
          //TODO restart the  node if it is not connected to the network
          if (now - this.lastPeer >= 35000) {
            console.log("No peers found, restarting node");
            await this.node.stop();
            this.node = await this.createNode();
          } else {
            console.log("No peers found, restarting node");
            await this.node.stop();
            this.node = await this.createNode();
            console.log(this.node);
            this.setChannel(this.channel);
            setInterval(this.checkAlive, 20000);
          }
          // sometimes we appear to be connected to the bootstrap nodes, but we're not, so let's try to reconnect
        } else {
          console.log("Still connected to bootstrap nodes");
        }
      },
  async processAnnounce(announce) {
      // process the recieved address
      const addr = new TextDecoder().decode(announce.data);
      if(this.nodeStatus !== 'Connected'){
        this.nodeStatus  = 'Connecting...'
      }
      
      if (announce.from == this.me.string) {
        console.log('Received my own announce, ignoring');
        return;
      }
     
      if (addr == "peer-alive") {
        console.log(addr);
        this.peerCount += 1;
        setTimeout(function () {
          this.peerCount -= 1;
        }, 15000);
        this.lastPeer = new Date().getTime();
      }
      // keep-alives are also sent over here, so let's update that global first
      this.lastAlive = new Date().getTime();
      if (addr == "keep-alive") {
        console.log(addr);
        this.lastAlive = new Date().getTime();
        return;
      }
      // get a list of peers
      this.peers = await this.node.swarm.peers();
      console.log(this.peers);
      for (let i in this.peers) {
        // if we're already connected to the peer, don't bother doing a circuit connection
        if (this.peers[i].peer == this.peer) {
          return;
        }
      }
      // log the address to console as we're about to attempt a connection
      console.log(addr);
      // connection almost always fails the first time, but almost always succeeds the second time, so we do this:
      try {
        await this.node.swarm.connect(announce.from);
      } catch (err) {
        console.log(err);
        await this.node.swarm.connect(announce.from);
      }

      this.nodeStatus = 'Connected'
    },
    async processRooms(msg){
      console.log(msg)
      const data = JSON.parse(new TextDecoder().decode(msg.data));
      for(let i = 0; i < this.rooms.length; i++){
        if(!data.id){
          return;
        }
        if(this.rooms[i].id === data.id){
          console.log('Already in rooms')
          return
        }else{
          this.rooms.push(data);
        }
      }
      await this.node.pubsub.publish('agora.rooms', new TextEncoder().encode(JSON.stringify(this.channel)))
      
    },
    async createNode() {
      //create a node to be passed into the chat component
      const node = await Ipfs.create({
        repo: "ipfs-" + Math.random(),
        relay: {
          enabled: true,
          hop: {
            enabled: true,
          },
        },
        config: {
          Addresses: {
            //Replace with final node id for prodcution
            //https://github.com/libp2p/js-libp2p-webrtc-star/blob/master/packages/webrtc-star-signalling-server/DEPLOYMENT.md
            Swarm: [
              "/dns4/agorachat.xyz/tcp/443/wss/p2p-webrtc-star",
              "/dns4/agorachat.xyz/tcp/443/wss/p2p-webrtc-star",
              "/dns4/agorachat.xyz/tcp/9090/wss/p2p-webrtc-star",
              "/dns6/agorachat.xyz/tcp/9090/wss/p2p-webrtc-star",
              "/dns6/agorachat.xyz/tcp/4430/wss/p2p/12D3KooWAGa2hvWZFXiCUjLFgNi4rD75gGLsPdSTxH2HnmUWuKin",
              "/dns4/agorachat.xyz/tcp/4430/wss/p2p/12D3KooWAGa2hvWZFXiCUjLFgNi4rD75gGLsPdSTxH2HnmUWuKin",
            ],
          },
        },
      });
      console.log(node);
      this.id = await node.id();
      this.node = node;
      const status = node.isOnline() ? "online" : "offline";
      this.status = status;
      console.log(`Node status: ${status}, id: ${this.id.id}`);
      this.me = this.id.id;
      console.log(this.me);
      //subscribe and publish to announce circuit
      await node.pubsub.subscribe("announce-circuit", this.processAnnounce);
      console.log("subscribed to announce-circuit");
      for (let i = 0; i < 10; i++) {
        await node.pubsub.publish(
          "announce-circuit",
          new TextEncoder().encode("peer-alive")
        );
        setTimeout(function(){}, 1000)
      }
      setInterval(function () {
        
          node.pubsub.publish(
            "announce-circuit",
            new TextEncoder().encode("peer-alive")
          );
      }, 1000);
      setInterval(async function () {
        node.pubsub.publish(
          "announce-circuit",
          new TextEncoder().encode("keep-alive")
        );
        this.peers = await node.swarm.peers();
      }, 2000)
      
      this.setChannel(this.channel)
      this.rooms.push(this.channel);

      
      
      //listen for new rooms and announce our current room
      
      await node.pubsub.subscribe('agora.rooms', this.processRooms);
      await node.pubsub.publish('agora.rooms', new TextEncoder().encode(JSON.stringify(this.channel)))
      
      return node;
    },
    async signMessage(message){
      if(!window.ethereum) {
        alert("Please enable metamask");
        return;
      }
      try{
        await window.ethereum.send("eth_requestAccounts");
        const provider = new ethers.providers.Web3Provider(window.ethereum);
        const signer = provider.getSigner();
        const signature =   await signer.signMessage(message);
        const address = await signer.getAddress();
        const signedMessage = {
          alias: this.alias,
          message: message,
          signature: signature,
          address: address,
          time: new Date().toLocaleTimeString(),
          messageId: Math.floor(Math.random() * 1000000),
          from: this.id
        }
        return signedMessage
      }
      catch(err){
        alert("Please enable metamask");
        console.log(err)
      }
      return null
    },
    async  verifyMessage(data) {
      try{
        const signerAddress = await ethers.utils.verifyMessage(
        data.message,
        data.signature
      );
      if(signerAddress == data.address){
        return true;
      }else{
        return false;
      }
      }catch(err){
        console.log(err)
        return false;
      }
      
    },
    async sendMessage(message) {
      try{
        const signedMessage = await this.signMessage(message);
        if(signedMessage){
          const data = JSON.stringify(signedMessage);
          await this.node.pubsub.publish(this.channel.name, new TextEncoder().encode(data));
        }
      }
      catch(err){
        console.log(err)
      }
    },
    async recieveMessage(msg){
      const data = JSON.parse(new TextDecoder().decode(msg.data));
      if(this.verifyMessage(data)){
        for(let i = 0; i < this.blockList.length; i++){
          if(this.blockList[i] === data.address){
            return;
          }
        }
        this.messages.push(data);
      }else{
        return
      }
    },
    async setChannel(channel) {
      this.messages = [];
      this.channel = channel;
      console.log("Channel set to " + channel.name);
      await this.node.pubsub.publish('agora.rooms', new TextEncoder().encode(JSON.stringify(this.channel)))
      await this.node.pubsub.subscribe(channel.name, this.recieveMessage);
      this.channelJoined = true;
    },
    async createRoom(data){
      data.id = Math.floor(Math.random() * 10000);
      this.channel = data;
      await this.setChannel(data);
    },
  },
    async created() {
        const body = document.querySelector('body');
        body.style.margin = '0px';
        await this.createNode();
        console.log('node created');
    }
  }
</script>

<style>
.main {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  height: 87vh;
  width: auto;
  z-index: 1;
  background-color: black;
  color: white;
  align-content: center;
  justify-content: space-between;
}
.main h1 {
  border-bottom: 2px;
  border-bottom-style: solid;
  border-bottom-color: white;
}

.banner {
  margin: 0;
  padding: 0;
  display: flex;
  height: 13vh;
  flex-direction: row;
  width: 100%;
  z-index: 1;
  background-color: black;
  color: white;
  align-content: center;
  justify-content: space-between;
}
body {
  margin: 0px;
  padding: 0;
  height: 100vh;
  width: 100vw;
}
html {
  margin: 0px;
  padding: 0;
  height: 100%;
  width: 100%;
  font-family: "Roboto Mono", monospace;
}
</style>
