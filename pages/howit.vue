<template>
 <div class="module">
    <div class="banner">
      <Banner />
    </div>
    <div class="main">
        <h1 class="title">How it works</h1>
        
        <!-- Redo the first line -->

        <p class="text">AgoraChat is a ephemeral and pseudonymous chat app built on the Interplanetary File Systems (IPFS) decentralized network.
Chats are published over the network in chat rooms that can be created by users. Once a message is published, it never touches a centralized system. Each message is propagated through the use of IPFS PubSub in a completely decentralized manner. Anyone can publish messages to AgoraChat without using
the web app (although messages will only display on the web app if they  follow the proper format). Messages are published with a non-unique
alias as well as a cryptographic signature provided by a Metamask wallet. Each message is cryptographically verified once 
recieved. The front end is built as a static page with Nuxt. 
</p>
        <h2 class="sub-title">Chat</h2>
        <p class="text">The chat module displays messages received in the current room and allows users to send messages to their room. 
Each message displays: Sender Alias, Sender Public Key, Message Text  and a block button. While Aliases are not unique
and can be changed at will, public keys are linked to a private key stored in the users Metamask wallet. When sending a chat,
you will first be asked to connect your Metamask wallet, AgoraChat does not gain access to your wallet, only the ability to read the public key and 
request signatures. When you send a message, Metamask will ask for you to  verify your signature on the message. Messages are impermanent, they are not  stored by any central  service, only in the local memory of the users that were listening when the message was published. Messages from the past are not saved. The block button can be used to block messages incoming from a certain Public Key, any messages received will not be displayed. </p>
        
        <h2 class="sub-title">Info</h2>
        <p class="text">The info module displays info about your node. It shows the current room you are in as well as the current alias you are using.  Aliases are not unique and can be set to any value.  Below the alias tab is  your Node Id and your Node peers. A new IPFS node is created whenever you open the chat page. This node will attempt to join the IPFS network by bootstrapping to an AgoraChat node  which provides connections to other IPFS nodes and a circuit relay for NAT traversal. These bootstrap nodes can be created anyone and help to provide stability to the PubSub network. Once your node is created, it starts attempting to connect to other  AgoraChat user nodes through PubSub and starts listening on the channels related to the current room. By default the current room is the Agora General Chat.</p>
        
        <h2 class="sub-title">Explorer</h2>
        <p class="text">The explorer shows the current AgoraChat rooms available to join. Every room is ephemeral, meaning it only exists as long as it is being used. If no  users are connected to a room, it  will cease to exist. Each room consists of a name and a description, you can create rooms for any topic. Once a room is created, the user who created it will join the room and start advertising it to the network. Users can join rooms by clicking on them in the explorer.</p>
        
      
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