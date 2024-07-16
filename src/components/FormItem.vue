<script setup>
import { ref, computed } from 'vue'

const initialItem = { label: '', count: 1, purchased: false, highPriority: false }

const newItem = ref({ ...initialItem })

const characterCount = computed(() => newItem.value.label.length)

const emit = defineEmits(['submitItem'])

const submitItem = (item) => {
  emit('submitItem', item)
  newItem.value = { ...initialItem }
}
</script>

<template>
  <form class="add-item-form" @submit.prevent="submitItem(newItem)">
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
      <p class="counter">{{ characterCount }}/50</p>
    </div>
    <label class="w-fit">
      <input type="checkbox" v-model="newItem.highPriority" />
      High Priority
    </label>
    <button class="btn btn-primary" :disabled="newItem.label.length <= 0">Save item</button>
  </form>
</template>
