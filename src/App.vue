
<template>
<div class="wrapper">
  <h1>Weather app</h1>
  <p>Get weather in {{ city == "" ? " your city" : cityName }}</p>
  <input type="text" v-model="city" placeholder="Type your city">
    <button v-if="city != ''" @click="getWeather()">See weather</button>
    <button disabled v-else>Input city name</button>
    <p class="error">{{ error }}</p>

    <div v-if="info != null">
      <p > {{ this.info }}</p>
      <p > {{ weather }}</p>
      <p > {{ showTemp }}</p>
      <p > {{ showTempMin }}</p>
      <p > {{ showTempMax }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() { 
    return {
      city: "",
      error: "",
      info: null
    }
  },
  computed: {
    cityName() {
      return "\"" + this.city + "\"";
    },
    showTemp() {
      return "Temperature: " + this.info.main.temp;
    },
    showTempMin() {
      return "Temperature min: " + this.info.main.temp_min;
    },
    showTempMax() {
      return "Temperature max: " + this.info.main.temp_max;
    },
    weather() { 
      return "Weather: " + this.info.weather[0].main;
    }
  }, 
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Type for city name more than 1 symbols";
        return false;
      }
      this.error = "";

      const appid = '557722ec3842bae278742cdcfd76ebf9';
      let url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${appid}`
      axios.get(url)
        .then(res => this.info = res.data)

    }
  }
}
</script>

<style scoped>

.error {
  color: #e77700;
}
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: #1cb700;
  padding: 20px;
  text-align: center;
  color: #fff;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #004fb7;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;  
}

.wrapper input:focus {
  border-bottom-color: #fbdf0b;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:disabled {
  background: #746027;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

</style>
