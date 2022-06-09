<template>
    <select @change="onChange" v-model="selected" class="form-select mt-10 block w-full p-3 rounded focus:text-gray-700 bg-white bg-clip-padding bg-no-repeat border border-solid border-gray-300 focus:bg-white focus:border-green-700 focus:outline-none">
        <option disabled value=""> Select Country </option>
        <option v-for="country in countries" :value="country.ID">
            {{country.Country}}
        </option>
    </select>
</template>

<script setup>
import { ref } from 'vue'

const emits = defineEmits(['getCountry'])
const props = defineProps({
    countries: Array
})

const selected = ref(0)

function onChange() {
    // returns an object where country id is equals to the selected value
    const country = props.countries.find((item) => item.ID === selected.value)

    emits('getCountry', country)
}

</script>