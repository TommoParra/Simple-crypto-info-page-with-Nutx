<script setup>
const route = useRoute();
const { data } = await useFetch('/api/ticker/?id=' + route.params.id);
const coin = data.value[0]; 

</script>

<template>
    <Suspense>
      <template #default>
        <div v-if="coin" class="flex items-center justify-center min-h-screen bg-gray-900 text-white p-6">
          <div class="w-full max-w-3xl bg-gray-800 shadow-lg rounded-lg p-6">
            <h2 class="text-3xl font-bold text-center mb-6">{{ coin.name }} Details</h2>
            <div class="overflow-x-auto">
              <table class="w-full border-collapse border border-gray-700 rounded-lg">
                <thead>
                  <tr class="bg-gray-700 text-gray-300 uppercase text-sm leading-normal">
                    <th class="py-3 px-6 text-left">Symbol</th>
                    <th class="py-3 px-6 text-left">Rank</th>
                    <th class="py-3 px-6 text-left">Price – US $</th>
                    <th class="py-3 px-6 text-left">Market Cap – US $</th>
                  </tr>
                </thead>
                <tbody class="text-gray-100 text-sm font-light">
                  <tr class="border-b border-gray-600 hover:bg-gray-700 transition">
                    <td class="py-3 px-6">{{ coin.symbol }}</td>
                    <td class="py-3 px-6">{{ coin.rank }}</td>
                    <td class="py-3 px-6">${{ coin.price_usd }}</td>
                    <td class="py-3 px-6">${{ coin.market_cap_usd }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </template>
      <template #fallback>
        <div class="flex items-center justify-center min-h-screen bg-gray-900 text-white">
          <p class="text-lg font-semibold animate-pulse">Loading...</p>
        </div>
      </template>
    </Suspense>
  </template>
  