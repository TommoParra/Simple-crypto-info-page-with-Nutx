<script setup>
const { data } = await useFetch('/api/tickers/?limit=10');
console.log("API Response:", data.value);
</script>

<template>
    <div class="min-h-screen bg-gray-100 dark:bg-gray-900 text-gray-900 dark:text-gray-100 flex flex-col items-center justify-center p-6">
      <div class="w-full max-w-4xl bg-white dark:bg-gray-800 shadow-lg rounded-lg p-6">
        <h1 class="text-3xl font-bold text-center mb-6">Crypto Prices</h1>
  
        <div v-if="data && data.data" class="overflow-x-auto">
          <table class="w-full border-collapse border border-gray-300 dark:border-gray-700 rounded-lg">
            <thead class="bg-gray-200 dark:bg-gray-700">
              <tr>
                <th class="p-3 border-b">Name</th>
                <th class="p-3 border-b">Symbol</th>
                <th class="p-3 border-b">Price (USD)</th>
                <th class="p-3 border-b">Details</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="currency in data.data" :key="currency.id" class="hover:bg-gray-100 dark:hover:bg-gray-800 transition">
                <td class="p-3 border-b">{{ currency.name }}</td>
                <td class="p-3 border-b">{{ currency.symbol }}</td>
                <td class="p-3 border-b">${{ currency.price_usd }}</td>
                <td class="p-3 border-b">
                  <NuxtLink 
                    :to="'/currency/' + currency.id" 
                    class="text-blue-500 dark:text-blue-400 hover:underline"
                  >
                    View
                  </NuxtLink>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
  
        <p v-else class="text-center text-lg font-medium">Loading...</p>
      </div>
    </div>
  </template>
  
  