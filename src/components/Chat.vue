<script setup>
import { onMounted, reactive, ref } from 'vue';
let comment = reactive({ comment: []});
let commentData = ref('');

onMounted(() => {
  const api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
  fetch(api_url)
    .then((response) => response.json())
    .then((data) => {
        console.log(data);
        comment.comment = data;


    });
});

const newComment = () => {
    console.log(commentData.value);
    comment.comment.push({
        user: "Chelsea",
        text: commentData.value,
    })
    let data = {
        user: "Chelsea",
        text: commentData.value
    }
    
    const api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
    fetch(api_url, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify (data)
    })
    .then((response) => response.json())
    .then((data) => {
        console.log(data);
        comment.comment.push ({
            id: data.id,
            user: data.user,
            text: data.text
        });
    });
}

</script>

<template>
    <div class="comments">
        <div class="comments__header">
          <h3>Comments</h3>
          <div class="comment">
            <input type="text" v-model="commentData" placeholder="Comment here">
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