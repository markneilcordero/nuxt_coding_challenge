<template>
    <div>
        <h1>Blog Posts</h1>
        <input
            v-model="searchQuery"
            type="text"
            placeholder="Search posts..."
            class="search-bar"
        />
        <ul v-if="filteredPosts.length">
            <li v-for="post in filteredPosts" :key="post.id">
                {{ post.title }}
            </li>
        </ul>
        <p v-else>No posts found.</p>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useFetch } from '#app';

const searchQuery = ref('');
const { data: posts, pending } = useFetch('https://jsonplaceholder.typicode.com/posts');

const filteredPosts = computed(() => {
    return posts.value?.filter(post =>
        post.title.toLowerCase().includes(searchQuery.value.toLowerCase())
    ) || [];
});
</script>

<style scoped>
.search-bar {
    padding: 10px;
    margin-bottom: 20px;
    width: 100%;
    max-width: 400px;
    border: 1px solid #ddd;
    border-radius: 4px;
}
</style>