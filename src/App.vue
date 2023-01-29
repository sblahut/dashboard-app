<template>
  <div id="app" class="container">
    <div class="row mt-5" v-if="arrPositive.length > 0">
      <div class="col">
        <h2>Positive</h2>
        <line-chart 
        :chartData="arrPositive" 
        :options="chartOptions" 
        label="Postive">
        </line-chart>
      </div>
    </div>
  </div>
</template>

<style>

</style>

<script>
import axios from "axios"; 
import moment from "moment";

import LineChart from "./components/LineChart";

export default {
  name: "app",
  components: { LineChart },
  data() {
      return {
        arrDate: [],
        arrState: [],
        arrPositive: [],
        arrNegative: [],
        chartOptions: {
          responsive: true,
          maintainAspectRatio: false
      }
    };
},
async created() {
  const { data } = await axios.get("https://api.covidtracking.com/v1/us/current.json");
  
  data.forEach(d => {
    const date = moment(d.date, "YYYYMMDD").format("MM/DD");

    const {
      state,
      positive,
      negative
      
    } = d;

    this.arrState.push({date, total: state});
    this.arrPositive.push({date, total: positive});
    this.arrNegative.push({date, total: negative});

    console.log(this.arrPositive);
  })
}
}
</script>


