<script setup>
const { data } = await useFetch('/api/tickers/?limit=10');
console.log("API Response:", data.value);
</script>

<template>
    <main>
      <h1>Index Page</h1>
    
      <table border="1 px solid" v-if="data && data.data">
        <thead>
          <tr>
            <th>Name</th>
            <th>Symbol</th>
            <th>Price</th>
            <th>Details</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="currency in data.data" :key="currency.id">
            <td>{{ currency.name }}</td>
            <td>{{ currency.symbol }}</td>
            <td>{{ currency.price_usd }}</td>
            <td>
              <NuxtLink :to="'/currency/' + currency.id">{{ currency.id }}</NuxtLink>
            </td>
          </tr>
        </tbody>
      </table>
      <p v-else>Loading...</p>
    </main>
  </template>
  