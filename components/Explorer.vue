<template>
  <div class="module">
    <h1>Explorer</h1>
    <!-- Display all of the rooms and their descriptions -->
    <div v-for="room in rooms" v-bind:key="room.id" class="room">
      <div class="room-name">
        {{ room.name }}
      </div>
      <div class="room-description">
        {{ room.description }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rooms: Array,
  },
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