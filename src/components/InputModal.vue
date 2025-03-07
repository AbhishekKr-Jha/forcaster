
<script> 
export default {
  data() {
    return {
inputCity:''
    };
  },
  methods:{
    onSubmit(){
this.$emit('input-city-value',this.inputCity)
    }
  }
};


</script>


<template>

    <div  @click.stop class="internalComp flex flexC justifyC itemsC">
        <h1>Forcaster<i style="margin-left: 7px;" class="icon fa-solid fa-magnifying-glass"></i></h1>
       <input v-model="inputCity" type="text" placeholder="Enter the city "  />
   
    <p>{{ inputCity }}</p>
   
<button type="button"  @click="onSubmit" >Search</button>

    </div>

</template>


<style scoped>


.internalComp{
width: 400px;
height: 400px;
background: black;
border: 1px solid gray;
border-radius: 10px;
}
input{
    width: 300px;
    padding: 8px 10px;
    border-radius: 5px;
    outline: none;
    border: 1px soli gray;
    margin: 35px 0;
}

/* option{ 
  padding: 8px;
  border: 1px solid gray;
  border-radius: 4px;
  outline: none;
} */


button{
    padding: 10px 22px;
    border-radius: 6px;
    border: 1px solid gray;
    cursor: pointer;
    color: white;
    background: transparent;
    /* margin-top: 46px; */
}


</style>