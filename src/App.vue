<template>
    <div>
        <div class="book-section">
          <p>by <a href="https://github.com/RiadJoul/WeatherAPI" target="_blank">Github</a></p>
          <div class="container">
            <div class="right">
              <figure class="back" id="back-cover" style="background-image: url('./assets/lightning.jpg');"></figure>
              <figure class="front" style="background-color:#171717;">
                <div class="info-side">
                  <div class="today-info-container">
                      <div class="today-info" style="color:white;">
                          <div class="precipitation"> <span class="title" style="padding-right:10px;">CONDITION </span><span class="value"> {{weather.forecast.forecastday[2].day.condition.text}}</span>
                              <div class="clear"></div>
                          </div>
                          <div class="humidity"> <span class="title">HUMIDITY</span><span class="value">{{weather.forecast.forecastday[2].day.avghumidity}} %</span>
                              <div class="clear"></div>
                          </div>
                          <div class="wind"> <span class="title">WIND</span><span class="value">{{weather.forecast.forecastday[2].day.avgvis_km}} km/h</span>
                              <div class="clear"></div>
                          </div>
                      </div>
                  </div>
                </div>
              </figure>
            </div>
            <div class="right">
              <!-- third day -->
              <figure class="back" style="color:white;" v-bind:style="{ 'background-image': 'url('+getUrl(weather.forecast.forecastday[2].day.condition.text)+')' }">
                <div class="weather-gradient"></div>
                  <div class="date-container">
                      <h2 class="date-dayname">{{ getDayFormat(weather.forecast.forecastday[2].date) }}</h2><span class="date-day">{{ getThirdDayDate() }}</span><i
                          class="location-icon" data-feather="map-pin"></i><span class="location">{{weather.location.name}}, {{weather.location.country}}</span>
                  </div>
                  <div class="weather-container"><i class="weather-icon" data-feather="sun"></i>
                      <h1 class="weather-temp">{{weather.forecast.forecastday[2].day.avgtemp_c}}°C</h1>
                      <h3 class="weather-desc">{{weather.forecast.forecastday[2].day.condition.text}} </h3>
                  </div>
              </figure>
              <figure class="front" style="background-color:#171717;">
                <div class="info-side">
                  <div class="today-info-container">
                      <div class="today-info" style="color:white;">
                          <div class="precipitation"> <span class="title" style="padding-right:10px;">CONDITION </span><span class="value"> {{weather.forecast.forecastday[2].day.condition.text}}</span>
                              <div class="clear"></div>
                          </div>
                          <div class="humidity"> <span class="title">HUMIDITY</span><span class="value">{{weather.forecast.forecastday[2].day.avghumidity}} %</span>
                              <div class="clear"></div>
                          </div>
                          <div class="wind"> <span class="title">WIND</span><span class="value">{{weather.forecast.forecastday[2].day.avgvis_km}} km/h</span>
                              <div class="clear"></div>
                          </div>
                      </div>
                  </div>
                </div>
              </figure>
            </div>
            <div class="right">
              <!-- second day -->
              <figure class="back" style="color:white;" v-bind:style="{ 'background-image': 'url('+getUrl(weather.forecast.forecastday[1].day.condition.text)+')' }">
                <div class="weather-gradient"></div>
                  <div class="date-container">
                      <h2 class="date-dayname">{{ getDayFormat(weather.forecast.forecastday[1].date) }}</h2><span class="date-day">{{ getSecondDayDate() }}</span><i
                          class="location-icon" data-feather="map-pin"></i><span class="location">{{weather.location.name}}, {{weather.location.country}}</span>
                  </div>
                  <div class="weather-container"><i class="weather-icon" data-feather="sun"></i>
                      <h1 class="weather-temp">{{weather.forecast.forecastday[1].day.avgtemp_c}}°C</h1>
                      <h3 class="weather-desc">{{weather.forecast.forecastday[1].day.condition.text}} </h3>
                  </div>
              </figure>
              <figure class="front" style="background-color:#171717;">
                <div class="info-side">
                  <div class="today-info-container">
                      <div class="today-info" style="color:white;">
                          <div class="precipitation"> <span class="title" style="padding-right:10px;">CONDITION </span><span class="value"> {{weather.current.condition.text}}</span>
                              <div class="clear"></div>
                          </div>
                          <div class="humidity"> <span class="title">HUMIDITY</span><span class="value">{{weather.current.humidity}} %</span>
                              <div class="clear"></div>
                          </div>
                          <div class="wind"> <span class="title">WIND</span><span class="value">{{weather.current.wind_kph}} km/h</span>
                              <div class="clear"></div>
                          </div>
                      </div>
                  </div>
                </div>
              </figure>
            </div>
            <div class="right">
              <figure class="back" style="color:white;" v-bind:style="{ 'background-image': 'url('+getUrl(weather.current.condition.text)+')' }">
                  <div class="weather-gradient"></div>
                  <div class="date-container">
                      <h2 class="date-dayname">{{ getDay() }}</h2><span class="date-day">{{ getDate() }}</span><i
                          class="location-icon" data-feather="map-pin"></i><span class="location">{{weather.location.name}}, {{weather.location.country}}</span>
                  </div>
                  <div class="weather-container"><i class="weather-icon" data-feather="sun"></i>
                      <h1 class="weather-temp">{{weather.current.temp_c}}°C</h1>
                      <h3 class="weather-desc">{{weather.current.condition.text}} </h3>
                  </div>
              </figure>
              <figure class="front" id="cover" style="background-image: url(./assets/afternoon.gif)">
                <h1>Weather In</h1>
                <p v-if="this.weather != null" style="font-weight:bold; color:#355C7D; font-size:20px;">{{weather.location.name}}, {{weather.location.country}}</p>
               <button v-if="this.isSearching == false" id="change" @click="changeCity()">Change City</button>
                <input v-if="this.isSearching == true" type="text" v-model="city" style="opacity:0.3; border-radius:10px;">
                <button v-if="this.isSearching == true" @click="searchWeather()" style="float:right; padding:2px; position:relative; top:-12px;">✔️</button>
                <p style="font-weight:bold; margin-top:40px; padding-left:140px">By : Riad Joul</p>
              </figure>
            </div>
          </div>
          <button v-if="this.bookPage <= 4 && this.bookPage > 0" @click="bookPage--" onclick="turnLeft()">Prev</button>
          <button v-if="this.bookPage < 4" @click="bookPage++" onclick="turnRight()">Next</button>
          <br />
        </div>
      </div>
</template>

<script>
const axios = require('axios').default;

    export default {
        mounted() {
            this.getIpAddress();
            
        },
        data(){
            return {
                bookPage: 0,
                api_key: 'b5c036d13bb84a0d951230905210309',
                api_base: 'https://api.weatherapi.com/v1/forecast.json',
                userIp:null,
                city:'',
                weather:null,
                isSearching:false
            }
        },
        computed:{
            
        },
        methods:{
            getIpAddress(){
              fetch('https://api.ipify.org?format=json')
              .then(x => x.json())
              .then(({ ip }) => {
                  this.userIp = ip;
                  this.getLocation();
              });
            },
            getLocation(){
              axios.get(`https://ipfind.co/?ip=${this.userIp}&auth=d73d6a74-3241-4615-9522-7f9943c57a2b`)
              .then((res) => {
                this.city = res.data.city;
                this.searchWeather();
              })
            },
            searchWeather(){
                axios.get(`${this.api_base}?key=${this.api_key}&q=${this.city}&days=7&aqi=yes&alerts=no`)
                  .then((res) => {
                    this.weather = res.data;
                    this.isSearching = false;
                });
            },
            changeCity(){
              this.isSearching = true;
            },
            getDay: function () {
            let d = new Date();
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            let day = days[d.getDay()];
            return day;
            },
            getDate: function () {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return date + ' ' + month + ' ' + year;
            },
            getSecondDayDate: function () {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let date = d.getDate() + 1;
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return date + ' ' + month + ' ' + year;
            },
            getThirdDayDate: function () {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let date = d.getDate() + 2;
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return date + ' ' + month + ' ' + year;
            },
            getDayFormat(dayFormat){
              var date = new Date(dayFormat);
              return date.toLocaleDateString('en-EN', { weekday: 'long' });
            },
            getUrl(condition){
              switch(condition){
              //partly cloudy
              case 'Partly cloudy':
                return './assets/cloudy.jpg'
              break;
              //sunny
              case 'Sunny':
                return './assets/sunny.jpg'
              break;
              //clear
              case 'Clear':
                return './assets/clear.jpg'
              break;
              //snow
              case 'Snow':
                return './assets/snow.jpg'
              break;
              //rainy
              case 'Rainy':
                return './assets/rainy.png'
              break;
              //rainy
              case 'Patchy rain possible':
                return './assets/rainy.png'
              break;
              //rainy
              case 'Moderate rain':
                return './assets/rainy.png'
              break;
              //rainy
              case 'Heavy rain':
                return './assets/rainy.png'
              break;
              //windy
              case 'Windy':
                return './assets/windy.png'
              break;
              //Misty
              case 'Mist':
                return './assets/mist.jpg'
              break;
              default:
                return './assets/cloudy.jpg'
              }
            }
        }
    }
</script>
<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700,900&display=swap');

        body{
            margin:0;
            background-color: #343d4b;
            font-family: 'Montserrat', sans-serif;
        }
        *{
            box-sizing: border-box;
        }
        .book-section{
            height: 100vh;
            width: 100%;
            padding: 40px 0;
            text-align: center;
        }
        .book-section > .container{
            height: 500px;
            width: 600px;
            position: relative;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 2%;
            margin-bottom: 30px;
            perspective: 1200px;
        }
        .container > .right{
            position: absolute;
            height: 100%;
            width: 50%;
            transition: 0.7s ease-in-out;
            transform-style: preserve-3d;
        }
        .book-section > .container > .right{
            right:0;
            transform-origin: left;
            border-radius: 10px 0 0 10px;
        }
        .right > figure.front, .right > figure.back{
            margin: 0;
            height: 100%;
            width: 100%;
            position: absolute;
            left:0;
            top:0;
            background-size: 200%;
            background-repeat: no-repeat;
            backface-visibility: hidden;
            background-color: white;
            overflow: hidden;
        }
        .right > figure.front{
            background-position: right;
            border-radius: 0 10px 10px 0;
            box-shadow: 2px 2px 15px -2px rgba(0,0,0,0.2);
        }
        .right > figure.back{
            background-position: left;
            border-radius: 10px 0 0 10px;
            box-shadow: -2px 2px 15px -2px rgba(0,0,0,0.2);
            transform: rotateY(180deg);
        }
        .flip{
            transform: rotateY(-180deg);
        }
        .flip::before{
            content: "";
            position: absolute;
            top:0;
            left:0;
            z-index: 10;
            width: 100%;
            height: 100%;
            border-radius: 0 10px 10px 0;
            background-color: rgba(0,0,0,0.1);
        }
        button{
            border: 2px solid #41B883;
            background-color: transparent;
            color: #41B883;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
            transition: 0.3s ease-in-out;
        }
        button:focus, button:active{
            outline: none;
        }
        .book-section > p{
            color: rgba(0,0,0,0.7);
            font-size: 24px;
        }
        .book-section > p > a{
            text-decoration: none;
            color: #41B883;
        }
        button:hover{
            background-color: #41B883;
            color: #fff;
        }
        .front#cover, .back#back-cover{
            background-color: #41B883;
            text-align: left;
            padding: 0 30px;
        }
        .front#cover h1{
            color: #fff;
        }
        .front#cover p{
            color: rgba(0,0,0,0.8);
            font-size: 14px;
        }

        #change{
            border: 2px solid #E6896B;
            background-color: transparent;
            color: #ffffff;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
            transition: 0.3s ease-in-out;
        }
        #change:focus, #change:active{
            outline: none;
        }
        #change:hover{
            background-color: #E6896B;
            color: #fff;
        }

        .weather-gradient {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  border-radius: 25px;
  opacity: 0.8;
}
.date-container {
  position: absolute;
  top: 25px;
  left: 25px;
}
.date-dayname {
  margin: 0;
}
.date-day {
  display: block;
}
.location {
  display: inline-block;
  margin-top: 10px;
}
.location-icon {
  display: inline-block;
  height: 0.8em;
  width: auto;
  margin-right: 5px;
}
.weather-container {
  position: absolute;
  bottom: 25px;
  left: 25px;
}
.weather-icon.feather {
  height: 60px;
  width: auto;
}
.weather-temp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
}
.weather-desc {
  margin: 0;
}

.info-side {
  margin-top:50%;
  padding-left: 20px;
  position: relative;
  float: center;
  height: 100%;
  width: 110%;
  padding-top: 25px;
}
.today-info {
  padding: 15px;
  margin: 0 25px 25px 25px;
  border-radius: 10px;
}
.today-info>div:not(:last-child) {
  margin: 0 0 10px 0;
}
.today-info>div .title {
  float: left;
  font-weight: 700;
}
.today-info>div .value {
  float: center;
}

@media only screen and (max-width: 600px) {
  .book-section .container {
    height: 400px;
    width: 370px;
  }
}
</style>