<script setup lang="ts">
import { ref } from 'vue'

const sound = ref(false)
const audio = ref<HTMLAudioElement>()

const toggleSound = () => {
  sound.value = !sound.value
  if (audio.value) {
    if (sound.value) {
      audio.value.play()
    } else {
      audio.value.pause()
    }
  }
}
</script>

<template>
  <audio ref="audio" autoplay="true" controls volume="0.2" class="audio">
    <source src="../assets/sounds/sounds.mp3" type="audio/mpeg" />
  </audio>
  <img src="../assets/images/mute.svg" alt="logo" class="waves" @click="toggleSound" v-if="sound" />
  <img
    src="../assets/images/sounds.svg"
    alt="sound"
    class="waves"
    @click="toggleSound"
    v-if="!sound"
  />
</template>

<style scoped>
.waves {
  width: 3rem;
  position: fixed;
  top: 1rem;
  right: 2rem;
  opacity: 0.5;
  cursor: pointer;

  &:hover {
    opacity: 1;
  }
}
.audio {
  opacity: 0;
}
</style>
