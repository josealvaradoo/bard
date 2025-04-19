<script setup lang="ts">
import CharacterAvatar from '@/components/CharacterAvatar.vue'
</script>

<template>
  <h2>Synergy</h2>
  <section class="section">
    <CharacterAvatar character="miss" />
    <CharacterAvatar character="tristana" />
    <CharacterAvatar character="jhin" />
    <CharacterAvatar character="lucian" />
    <CharacterAvatar character="aphelios" />
  </section>
</template>

<style scoped>
.section {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
  margin-top: 4rem;
}
</style>
