<template>
    <div>
        <h1>{{ currentTemp }}</h1>
        <h1>{{ weather }}</h1>
    </div>
</template>

<script>
const URL = 'http://api.openweathermap.org/data/2.5/weather?zip=80202,us&APPID='
const WEATHER_KEY = 'bbaf3bdf18579f92c6e14825f5c839bb'
export default {
    data() {
        return {
            currentTemp: 'Temperature in F',
            weather: 'Weather Conditions'
        }
    },
    mounted() {
        fetch(URL + WEATHER_KEY)
            .then(response => response.json())
            .then(this.updateWeather)
    }, 
    methods: {
        updateWeather(data) {
            window.console.log(data)
        }
    }
}
</script>

<style lang="scss">

</style>