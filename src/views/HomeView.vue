<template>
  <main>
    <div>
      <h1>Hello {{ name }}</h1>
      <div v-if="comments.length">
        <h2>Comments:</h2>
        <ul>
          <li v-for="(comment, index) in comments" :key="index">
            {{ comment.text }} - <i>{{ comment.user }}</i>
          </li>
        </ul>
      </div>
      <div v-else>
        <p>No comments found.</p>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const name = ref("Marvellous");
const link = ref("https://simple-blog-back.onrender.com/comments");
const comments = ref([]);

async function fetchComment() {
  try {
    const response = await fetch(link.value);
    const data = await response.json();
    comments.value = data;
    console.log(comments.value);
  } catch (error) {
    console.error("Failed to fetch comments:", error);
  }
}

onMounted(() => {
  fetchComment();
});
</script>

<style scoped>
main {
  text-align: center;
  /* width: 100%;
  height: 100%; */
}
</style>