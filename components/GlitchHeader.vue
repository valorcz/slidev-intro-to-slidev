<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{ text: string }>()
const display = ref('')
const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890@#&'

onMounted(() => {
  let iteration = 0
  const interval = setInterval(() => {
    display.value = props.text
      .split('')
      .map((letter, index) => {
        if (index < iteration) return props.text[index]
        return chars[Math.floor(Math.random() * chars.length)]
      })
      .join('')

    if (iteration >= props.text.length) clearInterval(interval)
    iteration += 1 / 2 // Speed of decode
  }, 30)
})
</script>

<template>
  <h2 class="text-5xl font-bold uppercase tracking-tighter text-[var(--slidev-theme-primary)]">
    {{ display }}
  </h2>
</template>