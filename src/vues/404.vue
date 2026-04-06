<script setup lang="ts">
  import { useRouter } from 'vue-router';
  const router = useRouter()

</script>
<template>
  <div class="content">
    <section>
      <div class="section-title"><div class="bullet"></div>Oops! 404</div>
      <div class="intro-body">
        <div class="greetings">Page Not Found</div>
        <div class="action">
          <button @click="router.push('/')">Back Home</button>
        </div>
      </div>
    </section>
  </div>
</template>
<style scoped>
@import '@/assets/css/content.css';
section {
  height: unset;
  min-height: 90%;
  margin: 1em 0;
}
.action > button {
  font-size: 1em;
  padding: 0.4em 1em;
  border-radius: .5em;
  color: var(--accent-color);
  background: var(--dark-accent);
}
@media (orientation: landscape) {
  .action > button {
    font-size: 1em;
  }
}
</style>
