<template>
    <div class="posts-container">
        <h2>Posts</h2>
        <div v-if="loading">Loading posts...</div>
        <ul v-else>
            <li v-for="post in posts" :key="post.id" class="post-item">
                <h3>{{ post.title }}</h3>
                <p>{{ post.body }}</p>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const posts = ref([]);
const loading = ref(true);

const fetchPosts = async () => {
    try 
    {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        posts.value = await response.json();
    }
    catch (error)
    {
        console.log('Failed to fetch posts:', error);
    }
    finally
    {
        loading.value = false;
    }
};

onMounted(fetchPosts);
</script>

<style>
.posts-container {
    padding: 1rem;
}

.post-item {
    margin-bottom: 1rem;
}
</style>