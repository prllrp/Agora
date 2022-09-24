<template>
    <div class="module">
        <h1 class = "title">AGORA CHAT</h1>
        <div class="logos">
            <h2 class="logos">Built  with: </h2>
            <img src="../static/ipfs-logo.0ac81a5a.svg" alt="IPFS Logo">
            <img src="../static/Metamask-icon.svg" alt="Metamask Logo">
        </div>
        <div class="links">
            <NuxtLink to="/" class="chat">Chat</NuxtLink>
            <NuxtLink to='/' class="how">How it works</NuxtLink>
            <NuxtLink to='/about' class="about">About</NuxtLink>
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
        width: 100%;
    }

    .links{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: auto;
        margin: 5px;
        padding: 5px;
    }

    .logos{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        height: 100%;
        width: auto;
    }

    .logos img{
        height: 22%;
        width: auto;
    }

    h2{
        font-size: 1.5rem;
        color: #fff;
        font-weight: 400;
        margin: 0 1rem;
    }

    .title{
        font-size: 4em;
        font-weight: 600;
        color: white;
        margin-left: 5%;
        width: auto;
    }

    NuxtLink{
        font-size: 1.5rem;
        color: #fff;
        font-weight: 400;
        margin: 0 1rem;
        padding: 5px;
    }
    
</style>