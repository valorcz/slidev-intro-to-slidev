<script setup lang="ts">
// defineModel creates a two-way binding prop named 'count'
const counter = defineModel('count', {
  default: 0,
})
</script>

<template>
  <div flex="~" w="min" border="~ main rounded-md">
    <button
      border="r main" p="2" font="mono" outline="!none"
      hover:bg="gray-400 opacity-20"
      @click="counter -= 1"
    >
      -
    </button>
    <span m="auto" p="2">{{ counter }}</span>
    <button
      border="l main" p="2" font="mono" outline="!none"
      hover:bg="gray-400 opacity-20"
      @click="counter += 1"
    >
      +
    </button>
  </div>
</template>