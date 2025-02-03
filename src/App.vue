<!-- src/App.vue -->
@import "~@fortawesome/fontawesome-free/css/all.min.css";

<template>
  <div class="bg-gray-100 min-h-screen p-8 text-gray-800">
    <header class="mb-6">
      <h1 class="text-3xl font-bold mb-2">Saját Portfólió</h1>
      <p class="text-lg">Készítette: [A Te Neved]</p>
    </header>

    <section class="mb-10">
      <h2 class="text-2xl font-semibold mb-4">Bemutatkozás</h2>
      <p class="mb-4">
        Üdvözöllek a portfóliómon! Itt megtalálod a projektekhez használt technológiákat és
        könyvtárakat, valamint néhány látványos animációt.
      </p>
      <p>
        Vigyél rá az egérrel az alábbi szövegre, hogy megjelenjenek a használt technológiák ikonjai!
      </p>
    </section>

    <!-- Hover-trigger -->
    <div
      class="relative inline-block text-xl font-bold mb-6 hover-trigger"
      @mouseenter="showIcons"
      @mouseleave="hideIcons"
    >
      Használt Technológiák

      <!-- Ikonok a hover után -->
      <transition-group
        name="icon-fade"
        tag="div"
        class="absolute left-0 mt-2"
        style="white-space: nowrap"
      >
        <div
          v-for="(icon, index) in icons"
          :key="icon.name"
          v-show="iconsVisible"
          ref="iconRefs"
          class="inline-block mx-1"
        >
          <i :class="icon.class + ' text-2xl'"></i>
        </div>
      </transition-group>
    </div>

    <section class="mb-10">
      <h2 class="text-2xl font-semibold mb-4">Nyelvek, Könyvtárak</h2>
      <ul class="list-disc list-inside">
        <li>Vue.js</li>
        <li>Tailwind CSS</li>
        <li>anime.js</li>
        <li>Egyéb animációs library-k (GSAP, AOS, stb.)</li>
      </ul>
    </section>

    <footer class="mt-10">
      <p class="text-center text-sm text-gray-500">&copy; 2025 - A Te Neved</p>
    </footer>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
// anime import
import anime from 'animejs/lib/anime.es.js'

export default {
  setup() {
    const icons = ref([
      { name: 'Vue.js', class: 'fab fa-vuejs' },
      { name: 'Tailwind', class: 'fab fa-css3-alt' },
      { name: 'anime.js', class: 'fas fa-star' },
    ])

    const iconsVisible = ref(false)
    const iconRefs = ref([])

    function showIcons() {
      iconsVisible.value = true
      // Biztosítsuk, hogy a DOM már renderelődött
      // kis késleltetéssel meghívjuk az anime.js-t
      setTimeout(() => {
        anime({
          targets: iconRefs.value,
          translateX: (el, i) => [50 * (i + 1), 0],
          opacity: [0, 1],
          easing: 'easeOutExpo',
          delay: anime.stagger(100),
        })
      }, 0)
    }

    function hideIcons() {
      // Kifelé animáció
      anime({
        targets: iconRefs.value,
        translateY: [0, -20],
        opacity: [1, 0],
        easing: 'easeInExpo',
        duration: 300,
        complete: () => {
          iconsVisible.value = false
        },
      })
    }

    onMounted(() => {
      // Belépő animáció, pl. a főcím
      anime({
        targets: 'h1',
        translateY: [-50, 0],
        opacity: [0, 1],
        easing: 'easeOutExpo',
        duration: 1000,
      })
    })

    return {
      icons,
      iconsVisible,
      iconRefs,
      showIcons,
      hideIcons,
    }
  },
}
</script>

<style scoped>
.hover-trigger {
  cursor: pointer;
  transition: color 0.3s;
}
.hover-trigger:hover {
  color: #1da1f2;
}
</style>
