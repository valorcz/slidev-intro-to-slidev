<script setup lang="ts">
import { ref } from 'vue'
import { onSlideEnter } from '@slidev/client'

const props = defineProps<{ text: string }>()
const display = ref('')
const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890@#&'

onSlideEnter(() => {
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
  <h2 
    :data-text="display"
    class="glitch text-5xl font-bold uppercase tracking-tighter text-[var(--slidev-theme-primary)]"
  >
    {{ display }}
  </h2>
</template>

<style scoped>
/* Base positioning for the stack */
.glitch {
  position: relative;
  display: inline-block;
}

/* Create two copies of the text using the data-attribute.
  These will act as the RGB channels.
*/
.glitch::before,
.glitch::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
}

/* The 'Cyan' layer - shifted slightly left */
.glitch::before {
  color: #0ff;
  z-index: -1;
  transform: translate(-2px, 0);
  /* Optional: Add a clip animation for extra "jitter" */
  animation: glitch-anim-1 2s infinite linear alternate-reverse;
}

/* The 'Magenta' layer - shifted slightly right */
.glitch::after {
  color: #f0f;
  z-index: -2;
  transform: translate(2px, 0);
  animation: glitch-anim-2 3s infinite linear alternate-reverse;
}

/* Animations to randomly jitter the chromatic layers 
  (clip-path slices the text to create the jagged glitch look)
*/
@keyframes glitch-anim-1 {
  0% { clip-path: inset(20% 0 80% 0); }
  20% { clip-path: inset(60% 0 10% 0); }
  40% { clip-path: inset(40% 0 50% 0); }
  60% { clip-path: inset(80% 0 5% 0); }
  80% { clip-path: inset(10% 0 70% 0); }
  100% { clip-path: inset(30% 0 50% 0); }
}

@keyframes glitch-anim-2 {
  0% { clip-path: inset(10% 0 60% 0); }
  20% { clip-path: inset(80% 0 5% 0); }
  40% { clip-path: inset(30% 0 20% 0); }
  60% { clip-path: inset(10% 0 80% 0); }
  80% { clip-path: inset(40% 0 10% 0); }
  100% { clip-path: inset(50% 0 30% 0); }
}
</style>