<template>
  <b-container fluid>
        <div class="body">

            <b-row class="api-strip">
                <b-col cols="4">
                    <p>{{ temp }}&deg; {{ weatherData.weather[0].description }}</p>
                </b-col>
                <b-col cols="4">
                    <p>{{ theTime }}</P>
                </b-col>
                <b-col cols="4">
                    <p>{{ weatherData.name }}</p>
                </b-col>
                <b-col cols="4">
                    <h1>To Do's</h1>
                </b-col>
            </b-row>
        </div>
  </b-container>
</template>

<script>

    
    import { mapActions, mapGetters } from "vuex";

    export default {
        name: 'dashboard',
        components: {
            
        },
        data() {
            return {
                weatherData: [],
                temp: '',
                lat: '',
                lon: '',
                ampm: 'am'
            }
        },
        computed: mapGetters(['isAuthenticated', 'currentUser']),
        methods: {
            init() {
                
            },
        },
        created() {
            this.geolocation();
        },
        methods: {
            getWeather(url) {
                axios.get(url)
                    .then(response => {
                    this.weatherData = response.data;
                    this.temp = Math.floor(((this.weatherData.main.temp) - 273.15) * 9/5 + 32);
                    console.log(response.data);
                })
                .catch(error => {
                    console.log(error);
                });
            },
            geolocation() {
                navigator.geolocation.getCurrentPosition(position => {
                    this.lat = position.coords.latitude;
                    this.lon = position.coords.longitude;

                    this.getWeather(`https://cors-anywhere.herokuapp.com/http://api.openweathermap.org/data/2.5/weather?lat=${this.lat}&lon=${this.lon}&APPID=4184ae2eac1d3a7f63689ed17eb87201`);
                })
            },
        },
        computed: {
            theTime() {
                let today = new Date();
                let hour = today.getHours();
                let minutes = today.getMinutes();

                if (hour > 12) {
                    hour -= 12;
                    this.ampm = 'pm'
                }

                if (minutes < 10) {
                    minutes = '0' + minutes;
                }

                let todayNow = hour + ':' + minutes + this.ampm;
                return todayNow
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import "../../sass/_variables.scss";
    
    .body {
        background-image: url('https://source.unsplash.com/random');
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
        background-attachment: fixed;
        height: 100vh;
        width: 100vw
    }

    .api-strip {
        text-align: center;
        color: white;
        font-size: 1vw;
        background: black;
        opacity: .7;
        height: 100vh;
    }

    .to-do {
        text-align: center;
        color: white;
        font-size: 1vw;
        background: black;
        opacity: .7;
        height: 100vh;

    }

</style>