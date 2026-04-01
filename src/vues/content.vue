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
.content {
  display: flex;
  flex-direction: column;
  gap: 1em;
  width: 95%;
  margin: auto;
}

section {
  font-size: 4.3vw;
  border-radius: .5em;
  box-shadow: 0.2em 0.2em 0.3em #00000065;
  display: flex;
  align-items: start;
  padding: 1em;
  height: 100vh;
  background: var(--background-color);
  scroll-margin-top: 8.5vh;
}

.section-title {
  font-size: .85em;
  display: flex;
  align-items: center;
  gap: .5em;
  width: 100%;
}

.section-title > div.bullet {
  width: .6em;
  height: .6em;
  border-radius: 50%;
  background: var(--grey-color);
}
@media (orientation: landscape) {
  section {
    border-radius: 1em;
    font-size: calc((1vw + 1vh) * 0.8);
    scroll-margin-top: 3vh;
  }
}
</style>
