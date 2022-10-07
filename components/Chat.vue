<template>
  <div class="module">
    
      
          <h1>Chat</h1>
      <div class="chat-body" >
        <div v-for="message in messages" v-bind:key="message.messageId" class="chat-body-message">
          <div class="chat-body-alias">
            {{ message.alias}} 
            <div class="chat-body-message-time">
            {{ message.time }}
            </div>
          </div>
            <div class="chat-body-alias-address">
             <p>{{message.address}}</p>  <button v-if = "message.from !== nodeId" class="block" @click = "$emit('block', message.address)">Block</button>
            </div>
          <div class="chat-body-message-text">
            >>{{ message.message }}
          </div>
          
        </div>
      </div>
      <div class="chat-footer">
        <div class="chat-footer-input">
          <textarea v-model = 'message' name="chatbox" id="chatbox" cols="30" rows="10" class="input" placeholder="Type here..." v-on:keyup.enter = 'sendMessage'></textarea>
        </div>
        <div class="chat-footer-button" @click="sendMessage">
          <button>Send</button>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      message: "",
    };
  },
  props:{
    messages: Array,
    rooms: Array,
    defaultChannel: Object,
    nodeId : String,
  },
  methods:{
    async sendMessage(){
      //emit an event to the parent
      this.$emit('send-message', this.message);
      this.message = ''
    },
    async blockUser(){
      this.$emit('block', );
    }
  }
}
</script>

<style scoped>

  .chat-body{
    height: 57vh;
    width: 100%;
    background-color: #000;
    overflow: auto;
    border-bottom:2px white solid; 
  }

  .chat-body-message{
    border-bottom: 2px solid;
  }

  .chat-body-alias{
    background-color: #000;
    display: flex;
    flex-direction: row;
  }
  .chat-body-alias-address{
    font-size: 0.5rem;
    color: #fff;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .chat-body-message-time{
    font-size: 0.6rem;
    color: #fff;
    align-self: flex-end;
    padding-left: 5px;
  }

  .chat-footer{
    height: auto;
    width: 100%;
    background-color: #000;
    display: flex;
    flex-direction: column;
  
  }

  .chat-footer-input{
    height: 100%;
    width: 100%;
    background-color: #000;
    border: none;
    
    
  }

  .chat-footer-button button{
    height: 5vh;
    width: 100%;
    background-color: #000;
    color: white;
    margin: 0;
    font-family: 'Courier New', Courier, monospace;
    border-top: 2px solid white;
  }

  .chat-footer-input textarea{
    height: 15vh;
    width: 96%;
    background-color: #000;
    color: #fff;
    border: none;
    font-size: 1.5em;
    padding:  0 1em 0 0 ;
    align-self: flex-start;
    justify-self: flex-start;
    font-family: 'Courier New', Courier, monospace;
    writing-mode: vertical-lr;
    resize: none;
  }

  .block{
    padding-right: 5px;
    margin-right: 5px;
  }

  .module{
    height: auto;
    width: 33vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border: 2px;
    border-style: solid;
    border-color: #fff;
}

</style>