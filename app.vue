<script setup lang="ts">
const { data, pending } = useFetch('https://sheets.googleapis.com/v4/spreadsheets/1lO3HNOv0_jXH8bVWl33aCRCa-BmGlSlHjy0JIlMEMSQ/values/A2:I?key=AIzaSyBCL9IShJzo5MrEojaYHbfD1SlGPw13dJo')
const chartOptions = computed(() => ({
  chart: {
    id: "vuechart-example",
  },

  xaxis: {
    categories: data.value?.values.map(v => v[0]) ?? [],
    type: 'datetime'
  },

  fill: {
    type: 'gradient',
    gradient: {
      shade: 'light',
      type: "vertical",
      shadeIntensity: 1,
      opacityFrom: 0.7,
      opacityTo: 0.9,
      stops: [0, 100]
    }
  },
}))

const series = computed(() => [
  {
    name: 'diff',
    type: 'column',
    data: data.value?.values.map(v => +v[7]) ?? [],
  },
  {
    name: 'balance',
    type: 'area',
    data: data.value?.values.map(v => +v[8]) ?? [],
  },
])
</script>

<template>
  <div v-if="pending">
    <div class="flex items-center justify-center">
      <div class="spinner-border animate-spin inline-block w-8 h-8 border-4 rounded-full" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
  </div>
  <div v-else>
    <ClientOnly>
      <apexchart
        height="600"
        :options="chartOptions"
        :series="series"
      />
    </ClientOnly>
  </div>
</template>
