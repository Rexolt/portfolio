<script setup>
import anime from 'animejs'
import { onMounted } from 'vue'

onMounted(() => {
  anime({
    targets: '.animated-text',
    translateY: [-50, 0],
    opacity: [0, 1],
    easing: 'easeOutExpo',
    duration: 1000,
  })
})
</script>

<template>
  <h1 class="animated-text text-4xl font-bold text-center">Üdvözöllek a portfóliómon! 🎉</h1>
</template>
