<template>
    <div>
      <h2>Posts</h2>
      <ul>
        <li v-for="post in posts" :key="post.id">
          {{ post.title }}
        </li>
      </ul>
      <div class="pagination">
        <button :disabled="page === 1" @click="previousPage">Previous</button>
        <span>Page {{ page }}</span>
        <button :disabled="posts?.length < limit" @click="nextPage">Next</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, watchEffect } from 'vue';
  import { useFetch } from '#app';
  
  const page = ref(1);
  const limit = 10;
  
  // Fetch data using `useFetch`
  const { data: posts, refresh } = useFetch(() => 
    `https://jsonplaceholder.typicode.com/posts?_page=${page.value}&_limit=${limit}`
  );
  
  // Update the fetch when the page changes
  const nextPage = () => {
    page.value++;
    refresh();
  };
  
  const previousPage = () => {
    if (page.value > 1) {
      page.value--;
      refresh();
    }
  };
  </script>
  
  <style scoped>
  .pagination {
    margin-top: 20px;
    display: flex;
    gap: 10px;
    align-items: center;
  }
  </style>
  