<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const editing = ref(false)
const items = ref([
  { id: 1, label: 'apple', count: 1, purchased: true, highPriority: false },
  { id: 2, label: 'peers', count: 1, purchased: true, highPriority: false },
  { id: 3, label: 'orange', count: 1, purchased: false, highPriority: true }
])
const initialItem = { label: '', count: 1, purchased: false, highPriority: false }
const newItem = ref({ ...initialItem })
const newItemHighPriority = ref(false)

const addItem = () => {
  items.value.push({
    id: items.value.length + 1,
    ...newItem.value,
    highPriority: newItemHighPriority.value
  })
  console.log(items.value)
  newItem.value = { ...initialItem }
  newItemHighPriority.value = false
}

const doEdit = () => {
  editing.value = !editing.value
  newItem.value = { ...initialItem }
  newItemHighPriority.value = false
}

const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button class="btn" v-if="editing" @click="doEdit">Cancel</button>
    <button class="btn btn-primary" v-else @click="doEdit">Show</button>
  </div>
  <form class="add-item-form" v-if="editing" @submit.prevent="addItem">
    <input type="number" v-model.number="newItem.count" min="1" required />
    <input type="text" v-model.trim="newItem.label" placeholder="Add an item" required />
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <button class="btn btn-primary" :disabled="newItem.label.length <= 0">Save item</button>
  </form>
  <ul>
    <li
      v-for="item in items"
      :key="item.id"
      :class="{ strikeout: item.purchased, priority: item.highPriority }"
      @click="togglePurchased(item)"
    >
      {{ item.count + ' ' + item.label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>
