<script setup>
  //import VideoPlayer.vue
  import VideoPlayer from './components/VideoPlayer.vue'
  //import VideoDetails.vue
  import VideoDetails from './components/VideoDetails.vue'
  //import Chat.vue
  import Chat from './components/Chat.vue'
</script>

<template>
  <div class="app">
    <VideoPlayer />
    <div class="details">
    <VideoDetails />
    <Chat />
    </div>
  </div>
</template>

<style scoped>
  .app {
    display: grid;
    grid-template-columns: 8fr 4fr;
  
  }
  .details {
    grid-column: 2;
  }
</style>