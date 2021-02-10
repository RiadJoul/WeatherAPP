<template>
    <div>
        <div class="city-input" style="margin-bottom:30px; color:white; font-weight:bold;" :style="{ visibility: isVisible }">
            <label class="day-name" style="padding-right:30px;">City : </label>
            <input style="opacity:0.2;" type="text" v-model="city">
            <button v-on:click="searchWeather" style="width:30%; height:40px;" class="location-button">GET</button>
        </div>
        <div class="container" v-if="weather != 'undefined'">
            <div class="weather-side" v-bind:style="{ 'background-image': 'url('+getUrl+')' }">
                <div class="weather-gradient"></div>
                <div class="date-container">
                    <h2 class="date-dayname">{{ getDay() }}</h2><span class="date-day">{{ getDate() }}</span><i
                        class="location-icon" data-feather="map-pin"></i><span v-if="this.country != ''" class="location">{{ weather.name }}, {{ this.country }}</span>
                </div>
                <div class="weather-container"><i class="weather-icon" data-feather="sun"></i>
                    <h1 class="weather-temp">{{ this.temp }}°C</h1>
                    <h3 class="weather-desc">{{ this.description }}</h3>
                </div>
            </div>
            <div class="info-side">
                <div class="today-info-container">
                    <div class="today-info">
                        <div class="precipitation"> <span class="title">CONDITION </span><span class="value"> {{ weather.weather[0].main }}</span>
                            <div class="clear"></div>
                        </div>
                        <div class="humidity"> <span class="title">HUMIDITY</span><span class="value">{{ this.humidity }} %</span>
                            <div class="clear"></div>
                        </div>
                        <div class="wind"> <span class="title">WIND</span><span class="value">{{ this.wind }} km/h</span>
                            <div class="clear"></div>
                        </div>
                    </div>
                </div>
                <div class="week-container">
                    
                </div>
                <div class="location-container">
                    <button v-on:click="visibility = 'visible'" class="location-button"> <i data-feather="map-pin"></i><span>Change location</span></button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('loaded');
            this.searchWeather();
        },
        data(){
            return {
                visibility:'hidden',
                background_url: './assets/afternoon.gif',
                api_key: 'ea30c43d45da45eec1e2f75d1496ca11',
                api_base: 'https://api.openweathermap.org/data/2.5/',
                query: '',
                error: '',
                country: '',
                city:'Amsterdam',
                description:'',
                temp:'',
                humidity:'',
                wind: '',
                weather:[],
            }
        },
        computed:{
            isVisible(){
                return this.visibility
            },
            getUrl(){
                return this.background_url
            }
        },
        methods:{
            searchWeather(){
                fetch(`${this.api_base}weather?q=${this.city}&units=metric&APPID=${this.api_key}`)
                    .then(res => {
                     return res.json();
                    }).then(this.setResults)
            },
            setResults (results) {
                this.weather = results;
                this.country = this.weather.sys.country;
                this.description = this.weather.weather[0].description;
                this.temp = Math.round(this.weather.main.temp);
                this.humidity = this.weather.main.humidity;
                this.wind = Math.round(this.weather.wind.speed);

                //change background
                if(this.description === 'clear sky'){
                    this.background_url = './assets/clearSky.jpg'
                }

                if(this.description === 'scattered clouds'){
                    this.background_url = './assets/cloudy.jpg'
                }

                if(this.description === 'snow' || this.description === 'light snow'){
                    this.background_url = './assets/snow.jpg'
                }
                if(this.city === 'dubai'){
                    this.background_url = './assets/dubai.jpg'
                }
                else{
                    this.background_url = './assets/night.gif'
                }

            },
            getDay: function () {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return day;
            },
            getDate: function () {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return date + ' ' + month + ' ' + year;
            }
        }
    }

</script>
