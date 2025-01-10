<template>
    <div class="todo-container">
        <h2>To-Do App</h2>
        <form @submit.prevent="addTask">
            <input v-model="newTaskText" placeholder="Enter a new task..." />
            <button type="submit">Add Task</button>
        </form>

        <ul>
            <li v-for="task in tasks" :key="task.id" class="task-item">
                <label>
                    <input type="checkbox" v-model="task.completed" />
                    <span :class="{ completed: task.completed }">{{ task.title }}</span>
                </label>
                <button @click="deleteTask(task.id)">Delete</button>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useFetch } from '#app';

const { data: initialTasks } = useFetch('https://jsonplaceholder.typicode.com/todo?_limit=10');
const tasks = ref(initialTasks.value || []);
const newTaskText = ref('');

const addTask = async () => {
    if (!newTaskText.value.trim()) return;

    const newTask = {
        title: newTaskText.value,
        completed: false,
    };

    const response = await fetch('https://jsonplaceholder.typicode.com/todos', {
        method: 'POST',
        body: JSON.stringify(newTask),
        headers: { 'Content-Type': 'application/json'},
    });

    if (response.ok)
    {
        const savedTask = await response.json();
        tasks.value.push(savedTask);
        newTaskText.value = '';
    }
};

const deleteTask = (id) => {
    tasks.value = tasks.value.filter((task) => task.id !== id);
};
</script>

<style>
.todo-container {
    padding: 1rem;
}
input {
    margin-right: 0.5rem;
}
.completed {
    text-decoration: line-through;
}
</style>