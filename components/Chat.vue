<template>
  <div class="module">
    <div class="chat">
      <div class="chat-header">
        <div class="chat-header-title">
          <h1>Chat</h1>
        </div>
      </div>
      <div class="chat-body" >
        <div v-for="message in messages" v-bind:key="message.messageId" class="chat-body-message">
          <div class="chat-body-alias">
            {{ message.alias}} 
            <div class="chat-body-message-time">
            {{ message.time }}
            </div>
          </div>
            <div class="chat-body-alias-address">
              {{message.address}}
            </div>
            
          
          <div class="chat-body-message-text">
            >>{{ message.message }}
          </div>
          
        </div>
      </div>
      <div class="chat-footer">
        <div class="chat-footer-input">
          <input v-model="message"  type="text" placeholder="Type here ..." />
        </div>
        <div class="chat-footer-button" @click="sendMessage">
          <button>Send</button>
        </div>
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
  },
  methods:{
    async sendMessage(){
      //emit an event to the parent
      this.$emit('send-message', this.message);
      this.message = ''
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
    border-bottom:2px white solid; ;
  }

  .chat-body-alias{
    background-color: #000;
    display: flex;
    flex-direction: row;
  }
  .chat-body-alias-address{
    font-size: 0.5rem;
    color: #fff;
  }

  .chat-body-message-time{
    font-size: 0.6rem;
    color: #fff;
    align-self: flex-end;
    padding-left: 5px;
  }

  .chat-footer{
    height: 15vh;
    width: 100%;
    background-color: #000;
    display: flex;
    flex-direction: column;
  
  }

  .chat-footer-input{
    height: 100%;
    width: auto;
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

  .chat-footer-input input{
    height: 15vh;
    width: 32vw;
    background-color: #000;
    color: #fff;
    border: none;
    font-size: 1.5em;
    padding:  0 1em 0 0 ;
    align-self: flex-start;
    justify-self: flex-start;
    font-family: 'Courier New', Courier, monospace;
  }

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