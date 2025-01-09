<template>
    <div class="weather-container">
        <h2>Weather Info</h2>
        <input v-model="city" placeholder="Enter city name..." />
        <button @click="getWeatherData">Get Weather</button>

        <div v-if="loading">Loading...</div>
        <div v-if="error">{{ error }}</div>

        <div v-if="weather">
            <h3>City: {{ weather.name }}</h3>
            <p>Temperature: {{ weather.main.temp }}°C</p>
            <p>Condition: {{ weather.weather[0].description }}</p>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const city = ref('');
const weather = ref(null);
const loading = ref(false);
const error = ref(null);

const getWeatherData = async () => {
    if (!city.value.trim()) 
    {
        error.value = 'Please enter a city name';
        return;
    }

    loading.value = true;
    error.value = null;

    try
    {
        const apiKey = '2e48995559b52cdf9478a38341fee90d';
        const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city.value}&units=metric&appid=${apiKey}`);
        const data = await response.json();

        if (data.cod === 200)
        {
            weather.value = data;
        }
        else
        {
            error.value = data.message;
        }
    }
    catch (err)
    {
        error.value = 'Failed to fetch data';
    }
    finally
    {
        loading.value = false;
    }
};
</script>

<style>
.weather-container {
    padding: 1rem;
}

input, button {
    margin: 0.5rem 0;
}
</style>