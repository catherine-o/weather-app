<template>
    <div class='weather'>
        <p class='details'>{{ currentTemp }}</p>
        <p class='details'>{{ weatherConditions }}</p>
    </div>
</template>

<script>
const URL = 'http://api.openweathermap.org/data/2.5/weather?zip=80202,us&APPID='
const WEATHER_KEY = 'bbaf3bdf18579f92c6e14825f5c839bb'
export default {
    data() {
        return {
            currentTemp: '',
            weatherConditions: '',
        }
    },
    mounted() {
        fetch(URL + WEATHER_KEY)
            .then(response => response.json())
            .then(this.updateWeather)
            .catch(this.displayError)
    }, 
    methods: {
        updateWeather(data) {
            let kelvinTemp = data.main.temp
            this.currentTemp = this.convertToFarenheit(kelvinTemp)
            this.weatherConditions = data.weather[0].description
        },
        convertToFarenheit(temp) {
            //Kelvin to Farenheit 
            //° F = 9/5 (K - 273) + 32
            let farenheit = (9/5)*(+temp - 273) + 32
            return farenheit.toFixed(1) + '°F'
        },
        displayError() {
            this.currentTemp = 'No Internet Connection'
            this.weatherConditions = 'Please Try Again'
        }
    }
}
</script>

<style lang="scss">
.weather {
    width: 50%;
    margin: auto;
    border: 0.5px solid rgb(125, 217, 240);
    border-radius: 5px;
    display: flex;
    justify-content: space-evenly;
    flex-flow: row wrap;
    .details {
        font-size: 30px;
        padding: 10px;
    }
}
</style>