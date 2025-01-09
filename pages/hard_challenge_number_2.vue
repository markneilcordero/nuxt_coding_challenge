<template>
    <div class="tasks-container">
        <h2>Task Manager</h2>
        <form @submit.prevent="addTask">
            <input v-model="newTask" placeholder="Enter a new task..." />
            <button type="submit">Add Task</button>
        </form>

        <ul>
            <li v-for="task in tasks" :key="task.id">
                <label>
                    <input type="checkbox" v-model="task.completed" @change="saveTasks" />
                    <span :class="{ completed: task.completed }">{{ task.text }}</span>
                </label>
                <button @click="deleteTask(task.id)">Delete</button>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const newTask = ref('');
const tasks = ref([]);

const addTask = () => {
    if (!newTask.value.trim()) return;

    tasks.value.push({
        id: Date.now(),
        text: newTask.value,
        completed: false,
    });

    newTask.value = '';
    saveTasks();
};

const deleteTask = (id) => {
    tasks.value = tasks.value.filter(task => task.id !== id);
    saveTasks();
};

const loadTasks = () => {
    const savedTasks = localStorage.getItem('tasks');
    if (savedTasks)
    {
        tasks.value = JSON.parse(savedTasks);
    }
};

onMounted(loadTasks);
</script>

<style>
.tasks-container {
    padding: 1rem;
}

.completed {
    text-decoration: line-through;
}
</style>