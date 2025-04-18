<script setup lang="ts">
const arrow = new URL('../assets/images/arrow.webm', import.meta.url).href
</script>

<template>
  <div class="arrow">
    <video autoplay loop :src="arrow"></video>
  </div>
</template>

<style scoped>
.arrow {
  position: relative;
  z-index: 1;
  top: 0rem;
}
</style>
