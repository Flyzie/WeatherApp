<script>
const apiKey = import.meta.env.VITE_API_WEATHER_API_KEY;

export default{
    name: 'LongForecast',
    props:{
        forecastInfo: Array,
    },
    methods:{
        getIcon(forecast){
            return `https://openweathermap.org/img/wn/${forecast.weather[0].icon}@2x.png`
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="main_Display" v-for="forecast in forecastInfo">
            <div class="key_display">
                <img :src="getIcon(forecast)" alt="weather icon">
                <h1>{{ forecast.main.temp }}°C</h1>
                <h2>{{forecast.weather[0].description}}</h2>
            </div>
            <h2>{{ forecast.dt_txt.slice(0, 10) }}</h2>
        </div>
    </div>
</template>

<style scoped>

    .main_Display{
        background-color: rgb(194, 194, 194);
        border-radius: 20px;
        padding: 1.5rem;
        max-width: 20%;
    }

    .container{
        margin-top: 1rem;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 2rem;
        width: 100%;
    }
</style>