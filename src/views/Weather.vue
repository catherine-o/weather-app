<template>
    <div class='weather'>
        <p class='details'>{{ currentTemp }}</p>
        <p class='details'>{{ weatherConditions }}</p>
    </div>
</template>

<script>
const URL = 'https://api.openweathermap.org/data/2.5/weather?zip=80202,us'
const units = '&units=imperial' //to grab temperature in Fahrenheit
const WEATHER_KEY = '&APPID=bbaf3bdf18579f92c6e14825f5c839bb'
export default {
    data() {
        return {
            currentTemp: '',
            weatherConditions: '',
        }
    },
    mounted() {
        fetch(URL + units + WEATHER_KEY)
            .then(response => response.json())
            .then(this.updateWeather)
            .catch(this.displayError)
    }, 
    methods: {
        updateWeather(data) {
            let temperature = data.main.temp.toFixed(1)
            this.currentTemp = temperature + '°F'
            this.weatherConditions = data.weather[0].description
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
    width: 80%;
    margin: auto;
    display: flex;
    flex-flow: row wrap;
    justify-content: space-evenly;
    border: 0.5px solid rgb(125, 217, 240);
    border-radius: 5px;
    @media only screen and (min-width: 950px){
        width: 65%;
    }
    @media only screen and (min-width: 1250px){
        width: 50%;
    }
    .details {
        font-size: 45px;
        padding: 10px;
        @media only screen and (min-width: 550px){
            font-size: 35px;
            padding: 5px;
        }
    }
}
</style>