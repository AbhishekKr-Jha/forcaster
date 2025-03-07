
<script>
import ForecastWeather from './ForecastWeather.vue';
import ExtraWeatherInfo from './ExtraWeatherInfo.vue';
import { useDateFormatter } from "../composable/Formatter";

export default{
    name:'CurrentWeatherCard',
    props: {
    data: Object, 
  },
  components:{
ForecastWeather,
ExtraWeatherInfo
  },
  setup() {
    const { formatDay, formatTime,isToday,formatDate } = useDateFormatter();
    return { formatDay, formatTime,isToday,formatDate };
  },
  methods:{
  
  },
  watch: {
    data(newData) {
      console.log("Updated Data--:", newData?.forecast?.forecastday[0]?.hour); // Now prints actual data when available
    },
},
//   async created(){
// console.log("ok")
// console.log(this.data)
//     }
}



</script>



<template>
    
<div style="margin-top: 30px;" class="flex flexC justifyC itemsC">
<div style="" class="flex flexC justifyC itemsC">


    <div class="weatherBox flex flexC justifyC itemsC">
    <p style="font-size: 22px;text-wrap: wrap;">{{`${data?.location?.name} , ${data?.location?.region}`}}</p>
    <p style="font-size: 22px;margin-top: 5px;">( {{ formatDate(data?.location?.localtime) }} )</p>
    
<div style="padding: 8px;border-radius: 100%;width: 120px;height: 120px;position: relative;">
    <img width="120px" height="120px" :src="data?.current?.condition?.icon" />
    <span style="">{{ data?.current?.condition?.text }}</span>
</div>
<p style="font-size: 35px;">{{ data?.current?.temp_c }}॰ C</p>
<!-- <p>{{ formatDate(data?.location?.localtime) }}</p> -->
<!-- background-color:rgba(215, 213, 213,0.6); -->
</div>

<div style="gap: 20px;" class="flex  justifyC itemsC">

<ExtraWeatherInfo text="Wind" image="src/assets/Icons/ic_air.svg" :info="`${data?.current?.wind_kph} KMH`"  />
<ExtraWeatherInfo text="Humidity" image="src/assets/Icons/ic_humidity.svg" :info="`${data?.current?.wind_kph} %`"  />
<ExtraWeatherInfo text="UV Index" image="src/assets/Icons/uv.png" :info="`${data?.current?.uv}`"  />


</div>


</div>

<hr style="width: 50%;height: 2px;background-color: red;margin-top: 30px;">

<div  class="">

<ForecastWeather :forecastData="data?.forecast?.forecastday.slice(0,5)"  />

</div>


</div>


</template>



<style scoped>
.weatherBox{
width: 220px;
height: 220px;
/* border: 1px solid gray; */
}
p{
    text-align: center;
}

span{
    position: absolute;
    top: 40px;
    right: -30px;
    padding: 3px 20px;
    background: black;
    border-radius: 8px;
    border: 1px solid white;
}

</style>