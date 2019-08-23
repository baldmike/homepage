<template>
    <div id="navig">
        <b-navbar toggleable="md" type="light" variant="light" fixed="top">
            <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

            <b-collapse is-nav id="nav_collapse">

                <b-navbar-nav class="ml-auto">
                    <b-nav-item v-if="isAuthenticated" @click="logout" right>Logout</b-nav-item>
                </b-navbar-nav>

            </b-collapse>
        </b-navbar>
    </div>    
</template>

<script>

    import { mapActions, mapGetters } from "vuex";

    export default {
        name: "NavBar",
        data() {
            return {
                weatherData: [],
                temp: '',
            }
        },
        methods: {

            logout() {
                this.$store.dispatch('logout');
            },

        },
        computed: {
            
        },
            
        
        
        computed: mapGetters(['isAuthenticated']),

        mounted() {
            // axios.get('https://cors-anywhere.herokuapp.com/http://api.openweathermap.org/data/2.5/weather?zip=60641,us&APPID=4184ae2eac1d3a7f63689ed17eb87201')
            // .then((response) => {
            //     this.weatherData = response.data;
            //     this.temp = Math.floor((this.weatherData.main.temp) - 273.15) * 9/5 + 32;
            // })
            // .catch(error => {
            //     console.log("GET WEATHER ERROR: " + error);
            // });
        }
            
    }
</script>


<style>
    #navig {
        margin-bottom: 70px;
    }
</style>

