<script>
export default{
    name: 'MainDisplay',
    props:{
        location: String,
        weather: Object,
        temperature: Number,
        icon: null,
        date: String,
    }
}
</script>

<template>
    <div class="main_Display">
        <h1>{{ location }}</h1>
        <h2>{{ weather.description }}</h2>
        <div class="key_display">
            <img :src="icon" alt="weather icon">
            <h1>{{ temperature }}°C</h1>
        </div>
        <h2>{{ date }}</h2>
    </div>

</template>

<style scoped>
    .main_Display{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .key_display{
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .key_display > h1{
        padding: 1rem;
    }

</style>