<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{ text }}</h2>
        <div class="text-2xl mt-4 mb-10">
            {{ timestamp }}
        </div>
    </div>
</template>

<script setup>
import { computed } from '@vue/reactivity';
import moment from 'moment'

const props = defineProps({
    text: String,
    dataDate: String
})

const timestamp = computed(() => {
    return moment(props.dataDate).format('MMMM Do YYYY, h:mm:ss a')
})
</script>
