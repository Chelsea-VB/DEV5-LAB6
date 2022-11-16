<script setup>
import { onMounted, ref } from 'vue';

onMounted(() => {
  const api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
  fetch(api_url)
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
    });
});

</script>

<template>
    <div class="chat">

    </div>
</template>

<style scoped>

</style>