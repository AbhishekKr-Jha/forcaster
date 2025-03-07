<script>
import { useDateFormatter } from "../composable/Formatter";

export default {
  name: "HourlyWeather",
  props: {
    hourlyData: Array,
  },
  watch: {
    hourlyData(newData) {
      console.log("hoyrly  Data:", newData); // Now prints actual data when available
    },
    setup() {
    const { formatDay, formatTime,isToday } = useDateFormatter();
    return { formatDay, formatTime,isToday };
  },
  },
};
</script>

<template>
  <div class="hourlyViewContainer">
    <p
      style="font-weight: 600;text-align: center;padding: 8px 0;">
      Hourly Weather
    </p>

    <div class="hourlyViewScroller">
      <!-- height: 100px;width:100px; -->
      <div
        v-for="ele in hourlyData"
        :key="ele?.time"
        class="flex flexC justifyC itemsC hourlyBox"
      >
       

        <div class="flex itemsC justifyS hourlyCards">
          <img width="60px" :src="ele?.condition?.icon" />
          <div style="margin: 0 15px;" class="">
              <p> {{ ele?.time?.split(" ")[1] }}</p>
            <p> · {{ele?.condition?.text}}</p>
            <p>· {{ ele?.temp_c || "897" }}॰ C</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.hourlyViewContainer {
  position: absolute;
  top: 30px;
  margin-top: 20px;
  right: 50px;
  border: 1px solid gray;
  border-radius: 8px;
}
.hourlyViewScroller {
  width: 200px;
  height: 270px;

  padding: 3px;
  overflow-y: auto;

  scrollbar-width: none;
}

.hourlyViewScroller::-webkit-scrollbar {
  display: none; /* For Chrome, Safari, and Edge */
}

.hourlyBox {
  border: 2px solid gray;
  margin: 5px 0;
  border-radius: 8px;
}

p{
    font-size: 18px;
}

.hourlyCards {
  width: 100%;
  padding: 8px 10px;
}
</style>
