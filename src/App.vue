<script setup lang="ts">
import HeaderApp from './components/HeaderApp.vue';
import BodyApp from './components/BodyApp.vue';
import FooterApp from './components/FooterApp.vue';
</script>

<template>
  <div :style="{ width: '300px' }">
    <HeaderApp msg="This is the header" />
    <BodyApp msg="Hello" />
    <FooterApp msg="This is a Footer" class="footer-app" />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
