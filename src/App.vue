<script>
import MainDisplay from './components/MainDisplay.vue'
import Header from './components/Header.vue'
import LongForecast from './components/LongForecast.vue';

const apiKey = import.meta.env.VITE_API_WEATHER_API_KEY;

export default {
  name: 'App',
  components: {
    MainDisplay,
    Header,
    LongForecast,
  },
  data() {
    return {
      location: 'Los angeles',
      weather: {},
      temperature: Number,
      icon: null,
      date: new Date().toLocaleString(),
      forecastInfo: Array,
    }
  },
  methods:{
    async getWeather(location){
      const locData = await this.getLocation(location);
      const result = await fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${locData[0].lat}&units=metric&lon=${locData[0].lon}&appid=${apiKey}`);
      const data = await result.json();
      
      const resultForecast = await fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${locData[0].lat}&units=metric&lon=${locData[0].lon}&appid=${apiKey}`)
      const dataForecast = await resultForecast.json();


      console.log(data, locData);
      console.log(dataForecast);

      this.location = data.name;
      this.weather = data.weather[0];
      this.temperature = data.main.temp;
      this.icon = `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
      this.date = new Date().toLocaleString();
      this.forecastInfo = this.fillArray(dataForecast);

      return {location};
    },

    async updateLocation(newLocation){
      this.location = newLocation;
      this.getWeather(this.location);
    },

    async getLocation(location){
      const locResult = await fetch(`http://api.openweathermap.org/geo/1.0/direct?q=${location}&limit=1&appid=${apiKey}`)
      const locData = await locResult.json();
      return locData;
    },
    
    fillArray(data){
        const arr = [];
        for(let i=0; i<40; i = i + 8){
            arr.push(data.list[i]);
        }
        return arr;
    },

  },
  created(){
    this.getWeather(this.location);
  }


}
</script>

<template>
  <header>
    <Header  @update:location="updateLocation"></Header>
  </header>

  <main>
    <MainDisplay :location="location" :weather="weather" :temperature="temperature" :icon="icon" :date="date"></MainDisplay>
    <LongForecast :forecastInfo="forecastInfo"></LongForecast>
  </main>
</template>

<style scoped>
  main{
    display: flex;
    justify-content: center;
    flex-direction: column;
  }

  header{
    width: 100%;
    display: flex;
    justify-content: center;
    margin-bottom: 5rem;
  }
</style>
