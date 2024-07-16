<script setup>
import { toRefs } from 'vue'

const props = defineProps({
  item: Object
})

const { label, count, purchased, highPriority } = toRefs(props.item)
</script>

<template>
  <li :class="{ strikeout: purchased, priority: highPriority }">
    {{ count + ' ' + label }}
  </li>
</template>
