<template>
    <div>
        <h1 style="text-align: center;">Comparing the Maxico and Swedan GDP Indicators </h1>
    <canvas ref="chartCanvas"></canvas>
   
  </div>

</template>

<script setup>
definePageMeta({
  layout: "navbar",
});
import { onMounted, ref } from 'vue';
import Chart from 'chart.js/auto';
import  axios  from "axios";

const chartCanvas = ref(null);
let maxicoData = ref([]);
let swedanData=ref([])
let year=ref([])

onMounted(async () => {
    const api_key = 'ff101fa392eb4b6:fv8qetbrsvgz1ud'
      const response = await axios.get(`https://api.tradingeconomics.com/historical/country/mexico/indicator/gdp?c=${api_key}`)
      const response2 = await axios.get(`https://api.tradingeconomics.com/historical/country/sweden/indicator/gdp?c=${api_key}`)
   for (let index = 0; index < response.data.length; index++) {
     maxicoData.value.push (response.data[index].Value);
     const dateString = response.data[index].DateTime;
        const dateObject = new Date(dateString);
         year.value.push( dateObject.getFullYear());
        }
        for (let index = 0; index < response2.data.length; index++) {
            swedanData.value.push (response2.data[index].Value);
        }
  
  if (chartCanvas.value) {
    const ctx = chartCanvas.value.getContext('2d');

    const data = {
      labels: year.value, 
      datasets: [
        {
          label: 'Mexico GDP Indicator',
          data: maxicoData.value,
          borderColor: 'rgba(75, 192, 192, 1)',
          fill: false,
        },
        {
          label: 'Sweden GDP Indicator',
          data: swedanData.value,
          borderColor: 'rgba(255, 99, 132, 1)',
          fill: false,
        },
      ],
    };

    new Chart(ctx, {
      type: 'line',
      data: data,
      options: {
        responsive: true,
        scales: {
          x: {
            type: 'linear', 
            position: 'bottom',
          },
          y: {
            beginAtZero: true,
          },
        },
      },
    });
  }
});

</script>

<style lang="scss" scoped>

</style>