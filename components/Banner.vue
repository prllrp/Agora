<template>
    <div class="module">
        <h1 class = "title">AGORA CHAT</h1>
        <div class="links">
            <h2 class="chat">Chat</h2>
            <h2 class="how">How it works</h2>
            <h2 class="about">About</h2>
        </div>

    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
    .module{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }

    .links{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: 20%;
    }

    .title{
        font-size: 4em;
        font-weight: 600;
        color: white;
        margin-left: 5%;
    }
    
</style>