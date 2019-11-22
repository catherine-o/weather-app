<template>
    <div>
        <h1>{{ currentTemp }}</h1>
        <h1>{{ weatherConditions }}</h1>
    </div>
</template>

<script>
const URL = 'http://api.openweathermap.org/data/2.5/weather?zip=80202,us&APPID='
const WEATHER_KEY = 'bbaf3bdf18579f92c6e14825f5c839bb'
export default {
    data() {
        return {
            currentTemp: 'No Internet Connection',
            weatherConditions: 'Please try again',
        }
    },
    mounted() {
        this.checkConnection()
        fetch(URL + WEATHER_KEY)
            .then(response => response.json())
            .then(this.updateWeather)
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
        checkConnection() {
            window.console.log(window.navigator.onLine)
        }
    }
}
</script>

<style lang="scss">

</style>