<template>
  <div class="module">
    <h1>Explorer</h1>
    <!-- Display all of the rooms and their descriptions -->
    <div class="rooms">
      <div v-for="room in rooms" v-bind:key="room.name" class="room">
      <div class="room-name">
        <h3>Room Name:</h3>
        {{ room.name }}
      </div>
      <div class="room-description">
        
        <h3>Room Description:  </h3>
        {{ room.description }}
      </div>
      <div class="join-room">
        <button class = 'join-room-btn' @click = 'joinRoom(room.name,room.description)'>Join Room</button>
      </div>
    </div>
    </div>
    
    <!-- Button to add a new room with a  name  and description -->
    
    <div class="add-room">
      <h1 class="add-room-title">Add Room</h1>
      <div class="add-room__item">
        <div class="add-room__item-name">Name</div>
        <input class="add-room__item-input" v-model="newRoomName" />
      </div>
      <div class="add-room__item">
        <div class="add-room__item-name">Description</div>
        <input class="add-room__item-input" v-model="newRoomDescription" />
      </div>
      <div class="add-room__item">
        <button class="add-room__item-button" @click="addRoom">Add Room</button>
      </div>
  </div>
  </div>
</template>

<script>
export default {
  props: {
    rooms: Array,
  },
  data(){
    return {
      newRoomName: '',
      newRoomDescription: '',
    }
  },
  methods:{
    addRoom(){
      this.$emit('add-room', {
        name: this.newRoomName,
        description: this.newRoomDescription,
      })
      this.newRoomName = ''
      this.newRoomDescription = ''
    },
    joinRoom(name,description){
      this.$emit('join-room', {
        name: name,
        description: description,
      })
    }
  }
};

</script>

<style  scoped>
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

.room{
    height: auto;
    width: 33vw;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    border: 2px;
    border-style: solid;
    border-color: #fff;
    margin: 5px;
    
}

.add-room{
  align-self: flex-start;
}

.rooms{
  overflow-x:  hidden;
  overflow-y: auto;
}

.room-name{
  overflow: hidden;
  padding: 5px;
  margin: 5px;
}

.room-description{
  overflow: hidden;
  overflow-x:  hidden;
  overflow-y: auto;
}

.join-room-btn{
  
  padding: 0.5rem;
  margin: 0.5rem;
}

</style>