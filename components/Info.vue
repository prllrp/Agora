<template>
  <div class="module">
    <h1>Info</h1>
    <div class="chat-info">
      <div class="chat-info__item">
        <div class="chat-info-channel">Current Chat</div>
        <div class="chat-info-channel">{{ channel.name }}</div>
      </div>
      <div class="chat-info__item">
        <div class="chat-info-description">Chat Description</div>
        <div class="chat-info-description">{{ channel.description }}</div>
      </div>
      <div class="chat-info-peers">
        <div class="chat-info-peers">Chat Peers</div>
        <div class="chat-info-peers" v-bind:key = "peer" v-for="peer in chatPeers" >{{ peers }}</div>
      </div>
    </div>
    <div class="node-info">
      <!-- Display the info from the ipfs node -->
      <div class="node-info__item">
        <div class="node-info-id">Node ID</div>
        <div class="node-info-id">{{ nodeId }}</div>
    </div>
    <div class="node-info__item">
      <div class="node-info-status">Node Status</div>
      <div class="node-info-status">{{ nodeStatus }}</div>
  </div>
  <div class="node-info__item"> 
    <div class="node-info-peers">Node Peers</div>
    <div class="node-info-peers">{{ nodePeers.length }}</div>
    <div class="node-info-peers"  v-bind:key = 'peer' v-for="peer in nodePeers">{{peer.peer}}</div>
  </div>
  </div>
  </div>
</template>

<script>
export default {
  props:{
    channel: {
      type: Object,
      required: true,
    },
    chatPeers: {
      type: Array,
      required: true,
    },
    nodePeers:{
      type: Array,
      required: true,
      default: [],
    },
    nodeStatus:{
      type: String,
      required: true,
      default: 'Offline',
    },
    nodeId: {
      required: true,
    },
  }
}

</script>

<style scoped>
  .module{
    height: auto;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border: 2px;
    border-style: solid;
    border-color: #fff;
  }

</style>