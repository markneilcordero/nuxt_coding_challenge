<template>
    <button
        :type="type"
        class="btn"
        @click="onClick"
    >
        {{ label }}
    </button>
</template>

<script setup>
defineProps({
    label: {
        type: String,
        required: true,
    },
    type: {
        type: String,
        default: 'button',
    },
    onClick: {
        type: Function,
        required: false,
    },
});
</script>

<style scoped>
.btn {
    background-color: #4CAF50;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
}

.btn:hover {
    background-color: #45a049;
}
</style>