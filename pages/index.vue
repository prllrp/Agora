<template>
  <div class="root">
    <div class="banner">
      <Banner />
    </div>
    <div class="main">
      <Explorer />
      <Chat />
      <Info></Info>
    </div>
  </div>


</template>

<script>
import Explorer from '~/components/Explorer.vue';
import Chat from '~/components/Chat.vue';
import Info from '~/components/Info.vue';
import Banner from '../components/Banner.vue';
export default {
    name: "IndexPage",
    components: { Explorer, Chat, Info, Banner },
    onMount() {
        const body = document.querySelector('body');
        body.style.margin = '0px';
    }

}
</script>

<style>
  .main{
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
  .main h1{
    border-bottom: 2px;
    border-bottom-style: solid;
    border-bottom-color: white;
  }
  
  .banner{
    margin: 0;
    padding: 0;
    display: flex;
    height: 13vh;
    flex-direction: row;
    width: auto;
    z-index: 1;
    background-color: black;
    color: white;
    align-content: center;
    justify-content: space-between;
  }
  body{
    margin: 0px;
    padding: 0;
    height: 100%;
    width: 100%;
  }
  html{
    margin: 0px;
    padding: 0;
    height: 100%;
    width: 100%;
    font-family: 'Roboto Mono', monospace;
  }
  

  
</style>
