<script setup lang="ts">
import WelcomeText from '@/components/WelcomeText.vue'
import SmokeEffect from '@/components/SmokeEffect.vue'
import BardCharapter from '@/components/BardCharapter.vue'
import ArrowDown from '@/components/ArrowDown.vue'
</script>

<template>
  <main class="main">
    <section class="section">
      <div class="container">
        <WelcomeText />
      </div>
      <BardCharapter />
    </section>
    <ArrowDown />
    <SmokeEffect />
  </main>
</template>

<style scoped>
.main {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}
.section {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 50vh;
  width: 100%;
}
.section,
.arrow {
  top: 4rem;
  filter: blur(10px);
  animation: fadeIn 4s ease-in-out forwards;
}
.container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  left: 10rem;
}
@keyframes fadeIn {
  0% {
    filter: blur(10px);
    opacity: 0.2;
  }
  100% {
    filter: blur(0px);
    opacity: 1;
  }
}
</style>
