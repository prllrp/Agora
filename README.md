## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out the [documentation](https://nuxtjs.org).


# AgoraChat

## About
AgoraChat is an MVP for a decentralized chat room built by Patrick Lane. It tries to adresss three features that are fundamental for the free and open digital society that Web3 and Decentralized technologies promise, these features being that AgoraChat is Public, Pseudoanonymous, and Accountable.

### Public
AgoraChat is public in the sense that it is not controlled by any single entity and open for anyone to join. AgoraChat is built upon and hosted on IPFS (Interplanetary File System), a decentralized storage and communication network. Because the site is hosted on IPFS, anyone is able to copy the code and store it or modify it for themselves. Because AgoraChat uses the IPFS/Libp2p 'PubSub' system for communication, any IPFS or Libp2p node can send messages on the AgoraChat channels and the messages will be recieved the same as any message originating from the AgoraChat app (so long as the message is in a format compatible with the front-end)

### Pseudoanonymous
Agora chat offers pseudoanonymity. While your messages are in no way tied to your personal identity, they are tied to the Public/Private Key Pair stored in your Metamask wallet. Meaning that although users can change the alias they publish their messages with, the messages will be tied to the same Public Key and be verified to have come from that source. This cryptographic verification is completed twice, once by the IPFS node with Public/Private pair associated with the node id and once by the app with the Metamask Public/Private pair.

### Accountability
Accountability is the least fleshed out feature of AgoraChat. It is currently accomplished by choosing pseudoanonymity over true anonymity and the 'Block' button. By choosing pseudoanonymity, for users of AgoraChat this means that their word is only as good as the reputation of their name (or more accurately their Public Key). Where most current social platforms handle bans by instigating them system-wide, AgoraChat leaves the banning decision to the individual, and avoids infringing upon any individuals freedom of speech while also respecting the freedom to not listen.

### A very "M" VP
But these are primitive solutions for the massive problem of accountability and governance in decentralized networks, a problem that will need to be solved with great care and effort, lest our efforts to promote openness and freedom in the exchange of information fall into the same trap our forebearers did at the advent of the internet, letting centralized tendencies acquire control for the sake of gaining more users or making more profits. Now with the rise of Web3 technologies, there once again arises an opportunity to create systems based on freedom, equality and individualism. AgoraChat is an MVP for this future.



## How it works

AgoraChat is a ephemeral and pseduoanonymous chat app built on the Interplanetary File Systems (IPFS) decentralized network.
Chats are published over the network in chat rooms that can be created by users. Once a message is published, it never touches a centralized system. Each message is propagated through the use of IPFS PubSub in a completely decentralized manner. Anyone can publish messages to AgoraChat without using
the web app (although messages will only display on the web app if they  follow the proper format). Messages are published with a non-unique
alias as well as a cryptographic signature provided by a Metamask wallet. Each message is cryptographically verified once 
recieved. The front end is built as a static page with Nuxt. 


### Chat
The chat module displays messages recieved in the current room and allows users to send messages to their room. 
Each message displays: Sender Alias, Sender Public Key, Message Text  and a block button. While Aliases are not unique
and can be changed at will, public keys are linked to a private key stored in the users Metamask wallet. When sending a chat,
you will first be asked to connect your Metamask wallet, AgoraChat does not gain access to your wallet, only the ability to read the public key and 
request signatures. When you send a message, Metamask will ask for you to  verify your signature on the message. Messages are impermanent, they are not  stored by any central  service, only in the local memory of the users that were listening when the message was published. Messages from the past are not saved. The block button can be used to block messages incoming from a certain Public Key, any messages recieved will not be displayed. 


### Info
The info module displays info about your node. It shows the current room you are in as well as the current alias you are using.  Aliases are not unique and can be set to any value.  Below the alias tab is  your Node Id and your Node peers. A new IPFS node is created whenever you open the chat page. This node will attempt to join the IPFS network by bootstrapping to an AgoraChat node  which provides connections to other IPFS nodes and a circuit relay for NAT traversal. These bootstrap nodes can be created anyone and help to provide stability to the PubSub network. Once your node is created, it starts attempting to connect to other  AgoraChat user nodes through PubSub and starts listening on the channels related to the current room. By default the current room is the Agora General Chat.

### Explorer
The explorer shows the current AgoraChat rooms available to join. Every room is ephemeral, meaning it only exists as long as it is being used. If no  users are connected to a room, it  will cease to exist. Each room consists of a name and a description, you can create rooms for any topic. Once a room is created, the user who created it will join the room and start advertising it to the network. Users can join rooms by clicking on them in the explorer. 

