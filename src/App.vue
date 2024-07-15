<script setup>
import { ref, computed } from 'vue'

const header = ref('Shopping List App')

const characterCount = computed(() => {
  return newItem.value.label.length
})

const editing = ref(false)
const items = ref([
  { id: 1, label: 'apple', count: 1, purchased: true, highPriority: false },
  { id: 2, label: 'peers', count: 1, purchased: true, highPriority: false },
  { id: 3, label: 'orange', count: 1, purchased: false, highPriority: true }
])

const hidePurchased = ref(false)
const filteredItems = computed(() => {
  return hidePurchased.value ? items.value.filter((item) => !item.purchased) : items.value
})

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
    <h1 class="text-4xl font-bold">{{ header }}</h1>
    <button class="btn" v-if="editing" @click="doEdit">Cancel</button>
    <button class="btn btn-primary" v-else @click="doEdit">Show</button>
  </div>
  <form class="add-item-form" v-if="editing" @submit.prevent="addItem">
    <input type="number" class="w-20" v-model.number="newItem.count" min="1" max="99" required />
    <div class="relative flex-1">
      <input
        type="text"
        class="w-full"
        v-model.trim="newItem.label"
        placeholder="Add an item"
        maxlength="50"
        required
      />
      <p class="counter" v-if="editing">{{ characterCount }}/50</p>
    </div>
    <label class="w-fit">
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <button class="btn btn-primary" :disabled="newItem.label.length <= 0">Save item</button>
  </form>
  <ul id="shopping-list">
    <button class="btn btn-primary" @click="hidePurchased = !hidePurchased">
      Hide purchased item
    </button>
    <li
      v-for="item in filteredItems"
      :key="item.id"
      :class="{ strikeout: item.purchased, priority: item.highPriority }"
      @click="togglePurchased(item)"
    >
      {{ item.count + ' ' + item.label }}
    </li>
  </ul>
  <p v-if="!filteredItems.length">Nothing to see here</p>
</template>
