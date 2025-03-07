


<script> 
export default {
  props: {
    text: String,
    image: String, 
    info:String
  },
};

</script>


<template>
    
    <div style="margin-top: 10px;"   class="flex flexC justifyC itemsC infoContainer">
    <div class="">
        <img width="40px" :src="image"  />
    </div>
    <p style="margin: 5px 0">{{text}}</p>
    <p >{{info}}</p>
   
</div>

</template>



<style >

.infoContainer{
    border: 2px solid gray;
    border-radius: 8px;
    width: 110px;
    height: 110px;

}


</style>