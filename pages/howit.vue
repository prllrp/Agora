<template>
 <div class="module">
    <div class="banner">
      <Banner />
    </div>
    <div class="main">
        <h1 class="title">How it works</h1>
        
        <!-- Redo the first line -->

        <p class="text">AgoraChat is an MVP for a decentralized chat room built by Patrick Lane. It tries to adresss three features that are fundamental for the free and open digital society that Web3 and Decentralized technologies promise, these features being that AgoraChat is Public, Pseudoanonymous, and Accountable.</p>
        <h2 class="sub-title">Chat</h2>
        <p class="text">AgoraChat is public in the sense that it is not controlled by any single entity and open for anyone to join. AgoraChat is built upon and  hosted on IPFS (Interplanetary File System), a decentralized storage and communication network. Because the site is hosted on IPFS, anyone is able to copy the code and store it or modify it for themselves. Because AgoraChat uses the IPFS/Libp2p 'PubSub' system for communication, any IPFS or Libp2p node can send messages on the AgoraChat channels and the messages will be recieved the same as any message originating from the AgoraChat app (so long as the message is in a format compatible with the front-end)</p>
        
        <h2 class="sub-title">Info</h2>
        <p class="text">AgoraChat is public in the sense that it is not controlled by any single entity and open for anyone to join. AgoraChat is built upon and  hosted on IPFS (Interplanetary File System), a decentralized storage and communication network. Because the site is hosted on IPFS, anyone is able to copy the code and store it or modify it for themselves. Because AgoraChat uses the IPFS/Libp2p 'PubSub' system for communication, any IPFS or Libp2p node can send messages on the AgoraChat channels and the messages will be recieved the same as any message originating from the AgoraChat app (so long as the message is in a format compatible with the front-end)</p>
        
        <h2 class="sub-title">Explorer</h2>
        <p class="text">AgoraChat is public in the sense that it is not controlled by any single entity and open for anyone to join. AgoraChat is built upon and  hosted on IPFS (Interplanetary File System), a decentralized storage and communication network. Because the site is hosted on IPFS, anyone is able to copy the code and store it or modify it for themselves. Because AgoraChat uses the IPFS/Libp2p 'PubSub' system for communication, any IPFS or Libp2p node can send messages on the AgoraChat channels and the messages will be recieved the same as any message originating from the AgoraChat app (so long as the message is in a format compatible with the front-end)</p>
        
      
      </div>
 </div>
</template>

<script>
import Banner from '~/components/Banner.vue';
export default {
    components: { Banner }
}
</script>

<style >
.module{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: auto;
    height: 100%;
    background-color: black;
}
.module .main{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 50%;
    margin: 5px;
    padding: 5px;
}

body {
  margin: 0px;
  padding: 0;
  height: 100%;
  width: 100%;
}

html{
  overflow-y: scroll;
}
    
</style>