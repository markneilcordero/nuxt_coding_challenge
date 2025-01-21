<template>
    <div>
        <p v-if="loading">Loading users...</p>
        <p v-else-if="error">{{ error }}</p>
        <ul v-else>
            <li v-for="user in users" :key="user.id">{{ user.name }}</li>
        </ul>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const users = ref([]);
const loading = ref(true);
const error = ref(null);

onMounted(async () => {
    try
    {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        if (!response.ok) throw new Error('Failed to fetch users');
        users.value = await response.json();
    }
    catch (err)
    {
        error.value = err.message;
    }
    finally
    {
        loading.value = false;
    }
});
</script>