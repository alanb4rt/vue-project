<script setup>
import { ref, computed } from 'vue'
import ListItem from './components/ListItem.vue'
import FormItem from './components/FormItem.vue'

const header = ref('Shopping List App')

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

const addItem = (item) => {
  items.value.push({
    id: items.value.length + 1,
    ...item
  })
}

const doEdit = () => {
  editing.value = !editing.value
}

const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="header">
    <h1 class="text-4xl font-bold">{{ header }}</h1>
    <button class="btn btn-cancel" v-if="editing" @click="doEdit">Cancel</button>
    <button class="btn btn-primary" v-else @click="doEdit">Show</button>
  </div>
  <FormItem v-if="editing" @submitItem="addItem" />
  <button class="btn btn-primary" @click="hidePurchased = !hidePurchased">
    {{ hidePurchased ? 'Show all item' : 'Hide purchased item' }}
  </button>
  <ul id="shopping-list">
    <ListItem
      v-for="item in filteredItems"
      :key="item.id"
      :item="item"
      @click="togglePurchased(item)"
    />
  </ul>
  <p v-if="!filteredItems.length">Nothing to see here</p>
</template>
