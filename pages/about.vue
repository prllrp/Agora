<template>
 <div class="module">
    <div class="banner">
      <Banner />
    </div>
    <div class="main">
        <h1 class="title">About</h1>
        <img src="../static/debate.png" alt="Philosophers debating">
        <h3>"socrates, marcus aurelius, epictetus and diogenes debating in athens, photorealistic, black and white"
          -created by Midjourney AI
        </h3>
        <!-- Redo the first line -->

        <p class="text">AgoraChat is an MVP for a decentralized chat room built by Patrick Lane. It tries to adresss three features that are fundamental for the free and open digital society that Web3 and Decentralized technologies promise, these features being that AgoraChat is Public, Pseudoanonymous, and Accountable.</p>
        <h2 class="sub-title">Public</h2>
        <p class="text">AgoraChat is public in the sense that it is not controlled by any single entity and open for anyone to join. AgoraChat is built upon and  hosted on IPFS (Interplanetary File System), a decentralized storage and communication network. Because the site is hosted on IPFS, anyone is able to copy the code and store it or modify it for themselves. Because AgoraChat uses the IPFS/Libp2p 'PubSub' system for communication, any IPFS or Libp2p node can send messages on the AgoraChat channels and the messages will be recieved the same as any message originating from the AgoraChat app (so long as the message is in a format compatible with the front-end)</p>
        <h2 class="sub-title">Pseudoanonymous</h2>
        <p class="text">Agora chat offers pseudoanonymity. While your messages are in  no way tied to your personal identity, they are tied to the Public/Private Key Pair stored in your Metamask wallet. Meaning that although users can change the alias they publish their messages with, the messages will be tied to the same Public Key and be verified to have come from  that source. This cryptographic verification is completed twice, once by the IPFS node with Public/Private pair associated with the node id and once by the app with the Metamask Public/Private pair.</p>
        <h2 class="sub-title">Accountability</h2>
        <p class="text">Accountability is the least fleshed out  feature of AgoraChat. It is currently accomplished by choosing pseudoanonymity  over true anonymity and the 'Block'  button. By choosing pseudoanonymity, for users of AgoraChat this  means that their word is only as good as the reputation of their name (or more accurately their Public Key). Where most  current social platforms handle bans by instigating them system-wide, AgoraChat leaves the banning decision to the individual, and avoids infringing upon any  individuals freedom of speech while also respecting the freedom to not listen. </p>
        <h2 class="sub-title">A very "M"  VP</h2>
        <p class="text">But these are primitive solutions for the massive problem of accountability and governance in decentralized networks, a problem that will need to be solved with great care and effort, lest our efforts to promote openness and freedom in  the exchange of information fall into the same trap our forebearers did at the advent of the internet, letting centralized tendencies acquire control for the sake of  gaining more users or making more profits. Now with the rise of Web3 technologies, there once again arises an opportunity to create systems based on freedom, equality and individualism. AgoraChat is an MVP for this future. </p>
        <h2 class="sub-title">Made By</h2>
        Patrick Lane graduated from Texas A&M University in May 2022 with a BS in Electronic Systems Engineering Techonology and a Minor in Cybersecurity. Coursework included networking, internet infrastructure and cryptographic key systems. He was also an avid participant in Engineering Inc. a startup incubator  inside the school's engineering department where he pursued the development of a business related to one of his other passions, soccer coaching. But this business ultimately never  launched as he choose to focus his efforts towards learning web development and Web3 technologies in hopes of having a larger impact on the world.

He is currently looking for work. (especially at companies in the decentralized technologies industry) and can be reached at:

patricklane09@gmail.com

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