<script setup>
  import { ref, reactive, onMounted } from 'vue'
  import 'animate.css';

  let src = ref('')
  let videos = reactive({ videos: []})
  let animation = ref("")
  
  //onmounted
  onMounted(() => {
    let api_url = "/public/tiktok.json";
    fetch(api_url)
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        src.value = data.videos[0].video;
        videos.videos = data.videos;
      });
  });

  const nextVideo = () => {
    animation.value = "animate__fadeOut"
    setTimeout(() => {
      src.value = videos.videos[1].video
      animation.value = "animate__fadeIn"
    }, 1000);
  }

</script>

<template>
  <div class="video">
    <div class="controls">
      <a @click.prevent="nextVideo" href="#" class="controls_next">↓</a>
    </div>
    <video :class="animation" class="animate__animated" :src="src" controls autoplay muted>
    </video>
  </div>
</template>

<style scoped>
  .controls {
    position: absolute;
    right: 2em;
    top: 0;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .controls_next {
    font-size: 2em;
  }
  .video{
    position: relative;
  }
  video{
    max-width: 100%;
    max-height: 100vh;
  }
</style>