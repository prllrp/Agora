<template>
  <div class="module">
    <h1>Explorer</h1>
    <!-- Display all of the rooms and their descriptions -->
    <div v-for="room in rooms" v-bind:key="room.name" class="room">
      <div class="room-name">
        {{ room.name }}
      </div>
      <div class="room-description">
        {{ room.description }}
      </div>
      <div class="join-room">
        <button class = 'join-room-btn' @click = 'joinRoom(room.name,room.description)'>Join Room</button>
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
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border: 2px;
    border-style: solid;
    border-color: #fff;
}

</style>