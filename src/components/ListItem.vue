<script setup>
const props = defineProps({
  item: Object
})
</script>

<template>
  <li :class="{ strikeout: item.purchased, priority: item.highPriority }">
    {{ item.count + ' ' + item.label }}
  </li>
</template>
