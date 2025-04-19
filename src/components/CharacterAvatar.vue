<script setup lang="ts">
const { character } = defineProps<{
  character: string
}>()

const image = new URL(`../assets/images/${character}.webp`, import.meta.url).href
</script>

<template>
  <div class="avatar">
    <img :src="image" alt="Avatar" />
  </div>
</template>

<style scoped>
.avatar {
  width: 10rem;
  height: 10rem;
  border-radius: 100%;
  overflow: hidden;

  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
}
</style>
