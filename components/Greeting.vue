<template>
    <div class="greeting-container">
        <h2>Dynamic Greeting</h2>
        <input v-model="name" placeholder="Enter your name..." />
        <p>{{ greetingMessage }}</p>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const name = ref('');
const greetingMessage = computed(() => {
    return name.value.trim() ? `Hello, ${name.value}!` : 'Hello, Guest!';
});
</script>

<style>
.greeting-container {
    padding: 1rem;
}

input {
    margin-bottom: 1rem;
    padding: 0.5rem;
    width: 100%;
}
</style>