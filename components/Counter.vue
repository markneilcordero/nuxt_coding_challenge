<template>
    <div class="counter-container">
        <h2>Counter: {{ count }}</h2>
        <button @click="increment">Increment</button>
        <button @click="decrement" :disabled="count === 0">Decrement</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const count = ref(0);

const increment = () => {
    count.value++;
};

const decrement = () => {
    if (count.value > 0)
    {
        count.value--;
    }
};
</script>

<style>
.counter-container {
    text-align: center;
    padding: 1rem;
}

button {
    margin: 0.5rem;
    padding: 0.5rem 1rem;
}
</style>