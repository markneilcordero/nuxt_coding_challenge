<template>
    <div>
        <h2>To-Do List</h2>
        <input v-model="newTask" placeholder="Add a new task" />
        <button @click="addTask">Add Task</button>
        <ul>
            <li v-for="(task, index) in tasks" :key="index">
                <input type="checkbox" v-model="task.completed" />
                <span :style="{ textDecoration: task.completed ? 'line-through' : 'none'}">
                    {{ task.name }}
                </span>
                <button @click="deleteTask(index)">Delete</button>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const tasks = ref([]);
const newTask = ref('');

const addTask = () => {
    if (newTask.value.trim()) {
        tasks.value.push({ name: newTask.value, completed: false });
        newTask.value = '';
    }
};

const deleteTask = (index) => {
    tasks.value.splice(index, 1);
};
</script>