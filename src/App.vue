<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: 'apple', count: 1 },
  { id: 2, label: 'peers', count: 1 },
  { id: 3, label: 'orange', count: 1 }
])
</script>

<template>
  <h1>{{ header }}</h1>
  <u>
    <li v-for="item in items" :key="item.id">{{ item.count + ' ' + item.label }}</li>
    <!-- <li v-for="{ id, label, count } in items" :key="id">{{ count + ' ' + label }}</li> -->
  </u>
</template>
