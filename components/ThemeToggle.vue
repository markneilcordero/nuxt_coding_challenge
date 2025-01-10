<template>
    <div :class="themeClass" class="theme-container">
        <h2>Current Mode: {{ theme }}</h2>
        <button @click="toggleTheme">Toggle {{ theme === 'light' ? 'Dark' : 'Light' }} Mode</button>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const theme = ref('light');

const toggleTheme = () => {
    theme.value = theme.value === 'light' ? 'dark' : 'light';
    localStorage.setItem('theme', theme.value);
};

const themeClass = computed(() => `theme-${theme.value}`);

onMounted(() => {
    const savedTheme = localStorage.getItem('theme');
    if (savedTheme)
    {
        theme.value = savedTheme;
    }
});
</script>

<style>
.theme-container {
    padding: 1rem;
    text-align: center;
}
.theme-light {
    background-color: white;
    color: black;
}
.theme-dark {
    background-color: black;
    color: white;
}
button {
    margin-top: 1rem;
    padding: 0.5rem 1rem;
}
</style>