<script setup lang="ts">
import { ref, onMounted } from 'vue'
import CharacterAvatar from '@/components/CharacterAvatar.vue'

const h2 = ref<HTMLElement | null>(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.5 },
  )

  if (h2.value) {
    observer.observe(h2.value)
  }
})
</script>

<template>
  <section class="section">
    <h2 ref="h2" :class="{ animate: isVisible }">Synergy</h2>
    <div class="characters">
      <CharacterAvatar character="miss" />
      <CharacterAvatar character="tristana" />
      <CharacterAvatar character="jhin" />
      <CharacterAvatar character="lucian" />
      <CharacterAvatar character="aphelios" />
    </div>
  </section>
</template>

<style scoped>
h2 {
  opacity: 0;
}

h2.animate {
  animation: fadeIn 2s ease-in-out forwards;
}

.section {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 4rem;
  margin-bottom: 4rem;
}
.characters {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
}
</style>
