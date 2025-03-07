
<script>
import { useDateFormatter } from "../composable/Formatter";
export default{
    name:'ForecastWeather',
    props:{
        forecastData:Array
    },
    setup() {
    const { formatDay, formatTime,isToday } = useDateFormatter();
    return { formatDay, formatTime,isToday };  
  },
  methods:{
    getImagePath(name,imageUrl) {
        console.log("teh name is",name,imageUrl)
        if(name=="Sunny"){
    //   return require(`@/assets/Icons/${name}.svg` )
    return true
    }
      else{
        return false
      }
    }
  }
}


</script>


<template>
    <!-- <div class="horizontalScroller"> -->
    <div style="gap: 20px; margin-top: 30px;" class="flex justifyC itemsC horizontalScroller">
    <div v-for="ele in forecastData" :key="ele?.date" style="height:150px ;width:150px ;border: 2px solid gray;border-radius: 8px; flex-shrink: 0;" class="flex flexC justifyC itemsC">
    <div class="">
        <!-- <button @click="getImagePath(ele?.day?.condition?.text,ele.day?.condition?.icon)" type="button" >jhgsaj</button> -->
        <!-- <img src="./Icons/cloudy.svg"  /> -->
        <!-- getImagePath(ele?.day?.condition?.text)?`@/assets/Icons/${name}.png`: -->
        <img width="60px" :src="ele.day?.condition?.icon"  />
    </div>
    <p style="margin: 8px 0;">{{ ele?.day?.condition?.text }} ({{ ele?.day?.maxtemp_c }}॰ C )</p>
    <p>{{isToday(ele?.date)?"Today": formatDay(ele?.date) }}</p>
</div>
</div>
<!-- </div> -->
</template>


<style scoped>
.horizontalScroller {
  width: 100vw  ;
  overflow-x: auto;
  white-space: nowrap;
  padding:0 0px; 
  margin: 0;
  scroll-behavior: smooth;
}
</style>