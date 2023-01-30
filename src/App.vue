<template>
  <div id="app" class="container">
    <div class="row mt-5">
      <div class="col">
        <h1 class="text-center">COVID-19 DATA</h1>
      </div>
    </div>

    <Bar class="row mt-5" v-if="arrPositive.length > 0">
      <div class="col">
        <h2 class="text-center">Positive</h2>
        <Bar :data="arrPositive" :options="chartOptions" label="Postive" />
      </div>
    </Bar>

    <Bar class="row mt-5" v-if="arrNegative.length > 0">
      <div class="col">
        <h2 class="text-center">Negative</h2>
        <Bar :data="arrNegative" :options="chartOptions" label="Negative" />
      </div>
    </Bar>
  </div>
</template>

<style>

</style>

<script>
import axios from "axios";
import moment from "moment";
import { Bar } from "vue-chartjs";

import BarChart from "./components/LineChart.vue";

export default {
  name: "app",
  components: { BarChart },
  data() {
    return {
      arrDate: [],
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

    // console.log(data)
    data.forEach(d => {
      const date = moment(d.date, "YYYYMMDD").format("MM/DD");

      const {
        positive,
        negative
      } = d;

      this.arrPositive.push({ date, total: positive });
      this.arrNegative.push({ date, total: negative });
    });
  }
};
</script>


