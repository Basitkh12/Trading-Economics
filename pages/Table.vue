<template>
    <div>
      <label for="countrySelect" style="font-size: 20px; margin: auto;"> Select a Country To Show Its Table  :  </label>
      <select v-model="selectedCountry" @change="updateChart">
        <option v-for="country in countries" >
          {{ country }}
        </option>
      </select>
  
      <div>
        <h2>GDP Data for {{ selectedCountry }}</h2>
        <table class="custom-table">
          <thead>
            <tr>
              <th>Year</th>
              <th>GDP Value</th>
              <th>Category</th>
            <th>Frequency</th>
            <th>Last Updated</th>
            <th>Country</th>
            <th>Historical Data Symbol</th>

            </tr>
          </thead>
          <tbody>
            <tr v-for="dataItem in selectedCountryData" :key="dataItem.year">
              <td>{{ dataItem.year }}</td>
              <td>{{ dataItem.value }}</td>
              <td>{{ dataItem.category }}</td>
            <td>{{ dataItem.frequency }}</td>
            <td>{{ dataItem.LastUpdate }}</td>
            <td>{{ dataItem.country }}</td>
            <td>{{ dataItem.HistoricalDataSymbol }}</td>


            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script setup>
  definePageMeta({
  layout: "navbar",
});
  import axios from 'axios';
  
  const countries = ref(['Sweden', 'Mexico', 'New Zealand', 'Thailand']);
  let selectedCountry = ref(null);
  let selectedCountryData = ref([]);
  
  async function updateChart() {
  
    const api_key = 'ff101fa392eb4b6:fv8qetbrsvgz1ud';
    const response = await axios.get(`https://api.tradingeconomics.com/historical/country/${selectedCountry.value}/indicator/gdp?c=${api_key}`);
  
    selectedCountryData.value = response.data.map(item => ({
      year: new Date(item.DateTime).getFullYear(),
      LastUpdate:new Date(item.LastUpdate).getFullYear(),
      value: item.Value,
      category: item.Category,
    frequency: item.Frequency,
    country:item.Country,
    HistoricalDataSymbol: item.HistoricalDataSymbol
    }));
    selectedCountryData.value.splice(-1, 1);
  }
  </script>
  
  <style scoped>
.custom-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.custom-table th, .custom-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.custom-table th {
  background-color: #f2f2f2;
}

.custom-table tbody tr:nth-child(even) {
  background-color: #f9f9f9;
}

.custom-table tbody tr:hover {
  background-color: #ddd;
}
  </style>
  