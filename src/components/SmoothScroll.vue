<script setup>
import { onMounted } from 'vue'
import LocomotiveScroll from 'locomotive-scroll'

onMounted(() => {
  const scroll = new LocomotiveScroll({
    el: document.querySelector('[data-scroll-container]'),
    smooth: true,
  })
})
</script>

<template>
  <div data-scroll-container>
    <section class="h-screen flex items-center justify-center bg-gray-900 text-white">
      <h1 data-scroll class="text-5xl">Smooth Scroll Élmény 🚀</h1>
    </section>
    <section class="h-screen flex items-center justify-center bg-gray-800 text-white">
      <h1 data-scroll class="text-5xl">Görgess tovább!</h1>
    </section>
  </div>
</template>
