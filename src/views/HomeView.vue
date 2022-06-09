<template>
	<main v-if="loading" class="flex flex-col align-center justify-center text-center">
		<div class="text-gray-500 text-3xl mt-10 mb-6"> Fetching Data... </div>
		<img :src="loadingImage" class="w-24 m-auto" alt="loading image">
	</main>

	<main v-else>
		<DataTitle :text="title" :dataDate="dataDate" />
		<DataBoxes :stats="stats" />
		<CountrySelect @getCountry="getCountryData" :countries="countries" />

		<button v-if="stats.Country" @click="clearCountryData"
			class="bg-green-700 text-white rounded p-2 mt-8 focus:outline-none hover:bg-green-600">
			Clear Country
		</button>
	</main>
</template>

<script setup>
import DataTitle from '@/components/DataTitle.vue'
import DataBoxes from '@/components/DataBoxes.vue'
import CountrySelect from '@/components/CountrySelect.vue'
import { onMounted, ref } from 'vue';


const loadingImage = require('../assets/loading.gif')
const loading = ref(true)
const title = ref('Global')
const dataDate = ref('')
const stats = ref(null)
const countries = ref(null)


function getCountryData(country) {
	stats.value = country
	title.value = country.Country
}

async function clearCountryData() {
	loading.value = true
	const data = await fetchCovidData()
	title.value = 'Global'
	stats.value = data.Global
	loading.value = false
}

async function fetchCovidData() {
	const res = await fetch('https://api.covid19api.com/summary')
	const data = await res.json()
	return data;
}

onMounted(async () => {
	const data = await fetchCovidData()
	dataDate.value = data.Date
	stats.value = data.Global
	countries.value = data.Countries
	loading.value = false
})
</script>
