<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: 'apple', count: 1 },
  { id: 2, label: 'peers', count: 1 },
  { id: 3, label: 'orange', count: 1 }
])
const newItem = ref({ label: '', count: 1 })
const newItemHighPriority = ref(false)
</script>

<template>
  <h1>{{ header }}</h1>
  <div>
    <input type="number" v-model.number="newItem.count" min="1" />
    <input type="text" v-model.trim="newItem.label" placeholder="Add an item" />
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority:
    </label>
  </div>
  <u>
    <li v-for="item in items" :key="item.id">{{ item.count + ' ' + item.label }}</li>
    <!-- <li v-for="{ id, label, count } in items" :key="id">{{ count + ' ' + label }}</li> -->
  </u>
</template>
