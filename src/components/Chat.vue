<script setup>
import { onMounted, reactive, ref } from 'vue';
let comment = reactive({ comment: []});

onMounted(() => {
  const api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
  fetch(api_url)
    .then((response) => response.json())
    .then((data) => {
        console.log(data);
        comment.comment = data;


    });
});

</script>

<template>
    <div class="comments">
        <div class="comments__header">
          <h3>Comments</h3>
          <div class="comment">
            <input type="text">
            <button @click="newComment">send</button>
            <ul class="comment_list">
              <li v-for="comment in comment.comment" :key="comment.id" >
                <h4>{{comment.user}}</h4>
                <p>{{comment.text}}</p>
              </li>
            </ul>
          </div>
        </div>
    </div>
  </template>

<style scoped>

.comment_list {
    display: flex;
    flex-direction: column-reverse;
    list-style: none;
}

</style>