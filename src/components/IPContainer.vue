<template>
  <div class="ipContainer">
    <div class="input-group">
      <input type="text" v-model="city" class="form-control" placeholder="Enter city name" autocomplete="off">
        <button class="btn btn-dark" @click.prevent="getCity" :disabled="isDisabled" type="button">Submit</button>
    </div>
    
    <div class="resultBox" v-show="isVisible">
      <ul class="details">
        <li class="h3">{{cityName}}, {{country}}</li>
        <li class="h4">{{desc}}<img v-bind:src="imgUrl"></li>
      </ul>
      <ul>
        <p class="fs-2">other details</p>
        <li class="h5">Temp is {{temp}} &deg;C</li>
        <li class="h5">Feels like {{feels}} &deg;C</li>
        <li class="h5">Max temp {{max}} &deg;C / min {{min}} &deg;C</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import VueAxios from 'vue-axios';
import axios from 'axios';
Vue.use(VueAxios,axios);
export default {
  name: 'IPContainer',
  data : function(){
    return {
      city:"",
      cityName:"",
      country:"",
      isVisible: false,
      temp: "",
      min: "",
      max:"",
      feels:"",
      desc:"",
      imgUrl:""
    };
  },
  computed: {
    isDisabled(){
      return this.city.length == 0;
    }
  },
  methods: {
    getCity () {
      Vue.axios.get('https://api.openweathermap.org/data/2.5/weather',{
        params:{
          q:this.city,
          appid: "7839972d87e610f9dbeb634aae00594f",
          units: "metric"
        }
      })
        .then(resp=>{
          let weatherData = resp.data;
          // console.warn(weatherData);
           if (weatherData.cod == 200) {
            const icon = weatherData.weather[0].icon;
            this.imgUrl = " http://openweathermap.org/img/wn/"+icon+"@2x.png";
            this.cityName = this.city;
            this.country = weatherData.sys.country
            this.temp = weatherData.main.temp;
            this.desc = weatherData.weather[0].description;
            this.feels = weatherData.main.feels_like;
            this.min = weatherData.main.temp_min;
            this.max = weatherData.main.temp_max;
            return this.isVisible = true;
           }
        })
        .catch(error =>{
          console.warn(error);
          alert("Please Enter Valid city Name");
          this.isVisible = false; 
         this.clear();
        })
    },
    clear () {
      this.city="";
      this.cityName="";
      this.temp= "";
      this.min= "";
      this.max="";
      this.feels="";
    }
  }
}
</script>

<style>

  ul{
    list-style: none;
    text-align: left;
    padding: 10px
  }
  .ipContainer{
    width: 370px;
    margin: 100px auto;
    padding: 5px;
    
    line-height: 2rem;
  }
  .details{
    background-color:rgba(245, 234, 22);
    color: rgba(71, 62, 24);
  }
  .resultBox{
    background-color: rgba(252, 249, 237);
    color: rgba(33, 33, 30);
  }
  p{
    text-align: center;
    font-weight: bold
  }
  
</style>