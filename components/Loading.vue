<template>
    
    
    <div class="main">
        <h1> AGORA CHAT</h1>
    <img src="../static/logo_200x200.png" alt="Agora Chat Logo">
    <img src="../static/agora.png" alt="Philosophers in an Agora">
    <h3>4 ancient greek philosophers debating in a digital agora, 2D, black and white, minimalist -created by Midjourney AI</h3>
    <h2>Loading Chat ... Please Wait</h2>
    </div>
    
  
</template>

<script>

import Banner from './Banner.vue';
export default {
    components: { Banner }
}
</script>

<style  scoped>
    .main{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100vw;
        background-color: #000;
        color: #fff;
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
</style>