<script setup lang="ts">
import WelcomeText from '@/components/WelcomeText.vue'
import SmokeEffect from '@/components/SmokeEffect.vue'
import BardCharacter from '@/components/BardCharacter.vue'
import ArrowDown from '@/components/ArrowDown.vue'
import SkillSection from '@/components/SkillSection.vue'
import SynergyChamps from '@/components/SynergyChamps.vue'
import FooterBox from '@/components/FooterBox.vue'
</script>

<template>
  <main class="main">
    <section class="section">
      <div class="welcome">
        <div class="container">
          <WelcomeText />
        </div>
        <div class="character">
          <BardCharacter />
        </div>
      </div>
      <ArrowDown />
    </section>
    <SkillSection />
    <SmokeEffect />
    <SynergyChamps />
  </main>
  <FooterBox />
</template>

<style scoped>
.main,
.section {
  width: 100%;
  min-height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}

.section {
  height: 100%;
  min-height: 100vh;
}

.welcome {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 50vh;
  width: 100%;
}
.welcome,
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
  left: 0rem;
  animation: moveInFromLeft 4s ease-in-out forwards;
}
.character {
  position: relative;
  width: 100%;
  height: 100%;
  right: 0rem;
  animation: moveInFromRight 4s ease-in-out forwards;
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
@keyframes moveInFromRight {
  0% {
    right: 0rem;
  }
  100% {
    right: 15rem;
  }
}
@keyframes moveInFromLeft {
  0% {
    left: 0rem;
  }
  100% {
    left: 15rem;
  }
}
</style>
