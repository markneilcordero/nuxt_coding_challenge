<template>
    <div class="users-container">
        <h2>User Directory</h2>
        <input v-model="search" placeholder="Search by name or email" />
        <div v-if="loading">Loading users...</div>
        <ul v-else>
            <li v-for="user in filteredUsers" :key="user.id" class="user-item">
                <strong>{{ user.name }}</strong>
                <p>{{ user.email }}</p>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useFetch } from '#app';

const search = ref('');
const { data: users, pending: loading } = useFetch('https://jsonplaceholder.typicode.com/users');

const filteredUsers = computed(() => {
    if (!users.value) return [];
    return users.value.filter(user =>
        user.name.toLowerCase().includes(search.value.toLowerCase()) ||
        user.email.toLowerCase().includes(search.value.toLowerCase())
    );
});
</script>

<style>
.users-container {
    padding: 1rem;
}

input {
    margin-bottom: 1rem;
    padding: 0.5rem;
    width: 100%;
}

.user-item {
    margin-bottom: 1rem;
}
</style>