<template>
  <div class="module">
    <h1 class = 'title'>Info</h1>
    <div class="chat-info">
      <h1 class="room-info">Room</h1>
      <div class="chat-info__item">
        <h2 class="chat-info-channel">Current Chat:</h2>
        <div class="chat-info-channel">{{ channel.name }}</div>
      </div>
      <div class="chat-info__item">
        <h2 class="chat-info-description">Chat Description:</h2>
        <div class="chat-info-description">{{ channel.description }}</div>
      </div>
    </div>
    <div class="alias">
      <h1 class="alias-info">Alias</h1>
      <div class="current-alias">Current Alias : {{alias}}</div>
      <input type="text" v-model='newAlias' class="new-alias">
      <button class="change-alias"  @click = 'changeAlias'>Change Alias</button>
    </div>
    <div class="node-info">
      <!-- Display the info from the ipfs node -->
      <div class="node-info__item">
        <h1 class="node-info-id">Node ID </h1>
        <div class="node-info-id">{{ nodeId }}</div>
    </div>
    <div class="node-info__item">
      <h1 class="node-info-status">Node Status</h1>
      <div class="node-info-status">{{ nodeStatus }}</div>
  </div>
  <div class="node-peers"> 
    <div class="node-info-peers">Node Peers</div>
    <div class="node-info-peers">{{ nodePeers.length }}</div>
    <div class="node-peers-list">
      <div class="node-info-peers-list"  v-bind:key = 'peer.peer.id' v-for="peer in nodePeers">{{peer.peer}}</div>
    </div>
    
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
    alias: {
      type: String,
      required: true,
    }
  },
  data(){
    return {
      newAlias: '',
    }
  },
  methods:{
    changeAlias(){
      this.$emit('change-alias', {
        alias: this.newAlias,
      })
    }
  }
}

</script>

<style scoped>

  .node-peers .node-info-peers-list{
    display: flex;
    flex-direction: column;
    overflow-x:  hidden;
    overflow-y: auto;
  }
  .chat-info{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: auto;
  }

  .module{
    height: auto;
    width: 32vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    border: 2px;
    border-style: solid;
    border-color: #fff;
  }

  .module .title{
    align-self: center;
  }

   



</style>