



<script>
import CurrentWeatherCard from './components/CurrentWeatherCard.vue'
import InputModal from './components/InputModal.vue'
import HourlyWeather from './components/HourlyWeather.vue'
import Loader from './components/Loader.vue'

export default{
  name:'App',
  data(){
return{
  weatherDetails:null,
  viewModal:false,
  loader:false
}
  },
  components:{
    CurrentWeatherCard,
    InputModal,
    HourlyWeather,
    Loader
  },
  methods:{
async fetchWeatherData(city){
  console.log("dat fetching strated")
  this.loader=true
  const res=await fetch(`http://api.weatherapi.com/v1/forecast.json?key=cd09a530ece24614bd775526250603&q=${city}&days=5&aqi=no&alerts=no`)
  

  console.log("the response coming from the data is",res)
  if (!res.ok) { 
      alert(res?.message || "Place can not be found!")
      this.loader=false
      return weatherDetails
    }

    const data = await res.json();
    console.log("dat fettching stopped as ",data)
    this.loader=false
    this.viewModal=false
  console.log("data has been found") 
  return data
},
toggleModal(){
 this.viewModal=false
},
async handleCityValue(cityVal){
 const newData= await this.fetchWeatherData(cityVal);
 this.weatherDetails={...newData}
  console.log("geot te hacfle city vakue",cityVal)
}
  },
  watch: {
    weatherDetails(newData) {
   console.log("the dat has been changed")
    },
  },
  async created(){
    this.weatherDetails = await this.fetchWeatherData('Kolkata');
    console.log(this.weatherDetails);
  }
    
}

</script>

<template>
<div class="container flex flexC itemsC">

  <div v-show="loader" style="width:100%;height:100%;position: absolute;top: 0;left: 0;background-color: black;z-index: 500;" class="">
    <Loader />
  </div>

  <HourlyWeather :hourlyData="weatherDetails?.forecast?.forecastday[0]?.hour" /> 
  <header style="margin: 20px 0; position: absolute; left: 20px;"  class=" flex  ">
    <h1 >Forcaster <i @click="viewModal=true" style="cursor: pointer;" class="icon fa-solid fa-magnifying-glass"></i></h1> 
  </header>

  <CurrentWeatherCard :data="weatherDetails"/>

  <div v-show="viewModal" @click="toggleModal" class="modalComp flex justifyC itemsC">
  <InputModal  @input-city-value="handleCityValue" />
</div>


</div>
</template>

<style >

.container{
width: 100%;
min-height: 100vh;
/* background: yellow; */
padding: 0 20px;
/* background: linear-gradient(135deg, #000066, #00008B, #2E0057, #000000); */
background: black;
color: white;

}
 


.flex{
  display: flex;
}
.itemsC{align-items: center;}
.justifyC{justify-content: center;}
.justifyS{justify-content: start;}
.flexC{flex-direction: column;}
.icon{
  font-size: 25px;
}

.modalComp{
    position: absolute;
    width: 100vw;
    height:100vh;
    background:  rgba(0, 0, 0, 0.5);
   
}

</style>