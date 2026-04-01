<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useEventListener } from '@vueuse/core'
import { useNavStore } from '@/stores/nav'

const body = ref<HTMLElement | null>(null)
const navStore = useNavStore()
onMounted(() => {
  body.value = document.body
})

useEventListener(body, 'scroll', () => {
  const sections = document.querySelectorAll('section')

  let current = 'home'

  sections.forEach((section) => {
    const rect = section.getBoundingClientRect()

    // section is in viewport (top half)
    if (rect.top <= window.innerHeight / 3.5) {
      current = section.id
    }
  })
  navStore.currentSection = current
})
</script>


<template>
  <div class="content">
    <section id="home">
      <div class="section-title"><div class="bullet"></div>Web Designer</div>
      <div class="intro-body">
        <div class="greetings">Hi, Khelawin</div>
        <div></div>
      </div>
    </section>
    <section id="skill">
      <div class="section-title"><div class="bullet"></div>Skills</div>
    </section>
    <section id="project">
      <div class="section-title"><div class="bullet"></div>Works</div>
    </section>
  </div>
</template>

<style scoped>
@import '@/assets/css/content.css';
</style>
