<template>
  <div class="module">
    <div class="chat">
      <div class="chat-header">
        <div class="chat-header-title">
          <h1>Chat</h1>
        </div>
      </div>
      <div class="chat-body">
        
      </div>
      <div class="chat-footer">
        <div class="chat-footer-input">
          <input type="text" placeholder="Message" />
        </div>
        <div class="chat-footer-button">
          <button>Send</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>

  .chat-body{
    height: 60vh;
    width: 100%;
    background-color: #000;
    overflow: auto;
  }

  .chat-footer{
    height: 15vh;
    width: 100%;
    background-color: #000;
    border: 2px;
    border-style: solid;
    border-color: #fff;
    display: flex;
  
  }

  .chat-footer-input{
    height: 100%;
    width: 100%;
    background-color: #000;
    float: left;
    
  }

  .chat-footer-button button{
    height: 100%;
    width: 100%;
    background-color: #000;
    float: right;
    color: white;
    margin: 0
  }

  .chat-footer-input input{
    height: 100%;
    width: 100%;
    background-color: #000;
    color: #fff;
    border: none;
    font-size: 1.5em;
    padding: 0 1em;
    align-self: flex-start;
  }

  .module{
    height: auto;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

</style>