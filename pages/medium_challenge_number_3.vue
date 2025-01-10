<template>
    <div class="users-container">
        <h2>User List</h2>
        <button @click="toggleSortOrder">Sort by Name: {{ sortOrder }}</button>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Phone</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in sortedUsers" :key="user.id">
                    <td>{{ user.name }}</td>
                    <td>{{ user.name }}</td>
                    <td>{{ user.phone }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useFetch } from '#app';

const { data: users, pending: loading } = useFetch('https://jsonplaceholder.typicode.com/users');
const sortOrder = ref('ascending');

const toggleSortOrder = () => {
    sortOrder.value = sortOrder.value === 'ascending' ? 'descending' : 'ascending';
};

const sortedUsers = computed(() => {
    if (!users.value) return [];
    return [...users.value].sort((a, b) => {
        if (sortOrder.value === 'ascending')
        {
            return a.name.localeCompare(b.name);
        }
        else
        {
            return b.name.localeCompare(a.name);
        }
    })
});
</script>

<style>
.users-container {
    padding: 1rem;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 0.5rem;
}
th {
    background-color: #f4f4f4;
}
button {
    margin-bottom: 1rem;
    padding: 0.5rem 1rem;
}
</style>