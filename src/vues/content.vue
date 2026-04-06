<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useEventListener } from '@vueuse/core'
import { useNavStore } from '@/stores/nav'
import clipboard from '@/assets/svg/clipboard.vue'
import download from '@/assets/svg/download.vue'
import { useOrientation } from "@/utils/orientation"
import * as Details from "@/constants/detail.json"

const UTILS_ORIENTATION = useOrientation()
const IS_LANDSCAPE = UTILS_ORIENTATION.IS_LANDSCAPE

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
const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText('torres.michael36@gmail.com')
    alert('Email Copied')
  } catch (err) {
    alert('Failed to copy:'+ err)
  }
}
</script>


<template>
  <div class="content">
    <section id="home">
      <div class="section-title">Web Designer</div>
      <div class="intro-body">
        <div>
          <div class="greetings">I'm Michael Torres</div>
          <div class="description">
            <div>Layout and Graphics</div>
            <div>Responsive Design</div>
            <div v-if="IS_LANDSCAPE">Mobile, Desktop, etc.</div>
            <div v-if="IS_LANDSCAPE">Reactive Layout (vue)</div>
          </div>
          <div class="intro-button">
            <button><span>CV</span><download/></button>
            <button @click="copyEmail"><span>Email</span><clipboard/></button>
          </div>
        </div>
        <div class="photo">
          <div>
            <img src="https://static.vecteezy.com/system/resources/thumbnails/057/357/660/small/cheerful-3d-avatar-with-glasses-for-digital-marketing-free-png.png" alt="avatar">
          </div>
        </div>
      </div>
      <div class="about-body">
        <div class="item" v-for="(item, index) in Details.about" :key="index">
          <div class="label">{{ Object.keys(item)[0] }}:</div>
          <div class="data">{{ Object.values(item)[0] }}</div>
        </div>
      </div>
      <div class="section-title">Education</div>
      <div class="education-body">
        <div class="item">
          <div class="logo">
            <img src="@/assets/img/logo/udemy.webp" alt="ubnhs">
          </div>
          <div class="name">
            <div>CSS, Bootstrap, Javascript</div>
            <div>ude.my/UC-a1c48038-82a7-4e66-aca2-9191215111a0</div>
          </div>
        </div>
        <div class="item">
          <div class="logo">
            <img src="@/assets/img/logo/tcu.webp" alt="logo">
          </div>
          <div class="name">
            <div>Taguig City University</div>
            <div>Bachelor in Computer Science</div>
          </div>
        </div>
        <div class="item">
          <div class="logo">
            <img src="@/assets/img/logo/ubnhs.webp" alt="ubnhs">
          </div>
          <div class="name">
            <div>Upper Bicutan National Highschool</div>
            <div>2008&ndash;2012</div>
          </div>
        </div>
        <div class="item">
          <div class="logo">
            <img src="@/assets/img/logo/ubes.webp" alt="ubnhs">
          </div>
          <div class="name">
            <div>Upper Bicutan Elementary School</div>
            <div>2002&ndash;2008</div>
          </div>
        </div>
      </div>
    </section>
    <section id="skill">
      <div class="section-title">Skills</div>
    </section>
    <section id="project">
      <div class="section-title">Project</div>
    </section>
  </div>
</template>

<style scoped>
@import '@/assets/css/content.css';
</style>
