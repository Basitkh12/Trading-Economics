<template>
    <div style="margin-top: 20px; ">
      <label for="countrySelect">Select a Country To See Its GDP : </label>
      <select v-model="selectedCountry" @change="updateChart">
        <option v-for="country in countries">
          {{ country }}
        </option>
      </select>
  
      <div>
        <canvas ref="chartCanvas"></canvas>
      </div>
    </div>
  </template>
  
  <script setup>
  definePageMeta({
  layout: "navbar",
});
  import axios from 'axios';
  import {  ref } from 'vue';
  import Chart from 'chart.js/auto';
  
  const chartCanvas = ref(null);
  const countries = ref(['Sweden', 'Mexico', 'New Zealand', 'Thailand']);
  let selectedCountry = ref(null);
  let selectedCountryData = ref([]);
  let chartInstance = null;
    
  async function updateChart() {

    if (chartInstance) {
      chartInstance.destroy();
    }
  
    const api_key = 'ff101fa392eb4b6:fv8qetbrsvgz1ud';
    const response = await axios.get(`https://api.tradingeconomics.com/historical/country/${selectedCountry.value}/indicator/gdp?c=${api_key}`);
  
    selectedCountryData.value = response.data.map(item => ({
      year: new Date(item.DateTime).getFullYear(),
      value: item.Value,
    }));
  
    if (chartCanvas.value) {
      const ctx = chartCanvas.value.getContext('2d');
  
      const data = {
        labels: selectedCountryData.value.map(item => item.year),
        datasets: [
          {
            label: `${selectedCountry.value} GDP`,
            data: selectedCountryData.value.map(item => item.value),
            borderColor: 'rgba(75, 192, 192, 1)',
            fill: false,
          },
        ],
      };
  
      chartInstance = new Chart(ctx, {
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
  }
  </script>
  
  <style scoped>
  
  </style>
  