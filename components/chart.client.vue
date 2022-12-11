
<script setup lang="ts">
const props = defineProps<{
  data?: {
    values: string[]
  }
}>()

const chartOptions = computed(() => ({
  chart: {
    id: "vuechart-example",
  },

  xaxis: {
    categories: props.data?.values.map(v => v[0]) ?? [],
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
    data: props.data?.values.map(v => +v[7]) ?? [],
  },
  {
    name: 'balance',
    type: 'area',
    data: props.data?.values.map(v => +v[8]) ?? [],
  },
])
</script>

<template>
  <apexchart
    height="600"
    :options="chartOptions"
    :series="series"
  />
</template>