<template>
  <main v-if="!loading">
    Show Data
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
    Fetching Data
    </div>
      <img :src="loadingImage" class="w-24 m-auto" alt="loading image">
  </main>
</template>

<script setup>
const { ref, watchEffect, onUpdated, onMounted }=require("@vue/runtime-core")
const url = 'https://api.covid19api.com/summary'
const loading = ref(true)
const title = ref('Global')
const dataDate = ref('')
const stat = {}
const countries = []
const loadingImage = require('../assets/logo.png')

async function fetchData() {
  const response = await fetch(url.value)
  data.value = await response.json()
  return data.value
}

// watchEffect(async () => {
//   const res = await fetch(url)
//   data.value = await res.json()
//   loading.value = false
//   console.log(data.value.Countries)
// })

</script>
