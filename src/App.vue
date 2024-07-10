<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: 'apple', count: 1 },
  { id: 2, label: 'peers', count: 1 },
  { id: 3, label: 'orange', count: 1 }
])
const initialItem = { label: '', count: 1 }
const newItem = ref({ ...initialItem })
const newItemHighPriority = ref(false)

const addItem = () => {
  items.value.push({ id: items.value.length + 1, ...newItem.value })
  newItem.value = initialItem
}
</script>

<template>
  <h1>{{ header }}</h1>
  <form class="add-item-form" @submit.prevent="addItem">
    <input type="number" v-model.number="newItem.count" min="1" required />
    <input type="text" v-model.trim="newItem.label" placeholder="Add an item" required />
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <button class="btn btn-primary">Save item</button>
  </form>
  <ul>
    <li v-for="item in items" :key="item.id">{{ item.count + ' ' + item.label }}</li>
    <!-- <li v-for="{ id, label, count } in items" :key="id">{{ count + ' ' + label }}</li> -->
  </ul>
</template>
