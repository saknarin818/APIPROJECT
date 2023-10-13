<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="container">
        <div class="innercontainer">
            <h2>{{ temperature }}<span>&#176;</span></h2>
            <p>{{ weatherDescription }}</p>

            <div v-if="showCloudy" class="weather-condition">
                <img src="../assets/Cloudy.jpg" alt="">
            </div>
            <div v-if="showRainy" class="weather-condition">
                <img src="../assets/rainy.jpg" alt="">
            </div>
            <div v-if="showStormy" class="weather-condition">
                <img src="../assets/strom.jpg" alt="">
            </div>
            <div v-if="showClear" class="weather-condition">
                <img src="../assets/Clear.jpg" alt="">
            </div>
            <div v-if="showDrizzle" class="weather-condition">
                <img src="../assets/drizzle.jpg" alt="">
            </div>
            <div v-if="showSnow" class="weather-condition">
                <img src="../assets/Snow.jpg" alt="">
            </div>
            <div v-if="showAtmosphere" class="weather-condition">
                <img src="../assets/fog.jpg" alt="">
            </div>

            <div class="input-container">
                <label for="latitude">Latitude</label>
                <input type="text" name="latitude" v-model="latitude">
            </div>
            <div class="input-container">
                <label for="longitude">Longitude</label>
                <input type="text" name="longitude" v-model="longitude">
            </div>
            <button @click="GetWeatherData()">Get Data</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        data(){
            return{
                weather:{},
                weatherDescription: '',
                showCloudy: false,
                showRainy: false,
                showStormy: false,
                showClear: false,
                showDrizzle: false,
                showSnow: false,
                showAtmosphere: false,
                temperature: '',
                latitude: '18.7965',
                longitude: '98.6601'
            }   

        },
    methods:{
        GetWeatherData(){
            axios.get('https://api.openweathermap.org/data/2.5/weather?lat='+ this.latitude +'&lon='+ this.longitude +'&appid=98cc7d640fa4bbf70f85de7486e1e642').then(
                response => {
                    console.log(response.data.weather)
                    let mainDescription = response.data.weather[0].main;
                    let descriptionString = response.data.weather[0].description;
                    this.weatherDescription = descriptionString.charAt(0).toUpperCase() + descriptionString.slice(1);
                    
                    this.temperature = response.data.main.temp;

                    switch(true){
                        case mainDescription == 'Clouds':
                            this.showCloudy = true;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Thunderstorm':
                            this.showCloudy = false;
                            this.showStormy = true;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Rain':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = true;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Clear':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = true;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Drizzle':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = true;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Snow':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = true;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Atmosphere':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = true;
                            break;
                    }
                }
            ).catch(error => {console.log(error)})
        }
    },
    mounted(){
        this.GetWeatherData();
    }
}
</script>

<style>
.container {
    width: 100%;
    display: flex;
    justify-content: center;
}

.innercontainer {
    width: 50%;
    background-color: rgb(253, 6, 47);
}
</style>