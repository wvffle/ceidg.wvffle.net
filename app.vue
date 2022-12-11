<script setup lang="ts">
const { data, pending } = useFetch<{ values: string[] }>('https://sheets.googleapis.com/v4/spreadsheets/1lO3HNOv0_jXH8bVWl33aCRCa-BmGlSlHjy0JIlMEMSQ/values/A2:I?key=AIzaSyBCL9IShJzo5MrEojaYHbfD1SlGPw13dJo', {
  default: () => ({ values: [] })
})
</script>

<template>
  <div v-if="pending">
    <div class="flex items-center justify-center">
      <div class="spinner-border animate-spin inline-block w-8 h-8 border-4 rounded-full" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
  </div>
  <div v-else-if="data">
    <Chart :data="data" />
  </div>
</template>
