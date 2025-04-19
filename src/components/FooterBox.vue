<script setup lang="ts"></script>

<template>
  <footer>
    <a href="https://github.com/josealvarado/bard" target="_blank">
      <img src="../assets/images/github.png" alt="Github" />
    </a>
    <a href="https://www.leagueofgraphs.com/es/summoner/lan/Frieck-LATAM" target="_blank">
      <img src="../assets/images/riot.png" alt="Riot" />
    </a>
  </footer>
</template>

<style scoped>
footer {
  padding: 7rem;
  display: flex;
  justify-content: center;
  gap: 1rem;

  img {
    width: 3rem;
    cursor: pointer;
    filter: grayscale(1);
    opacity: 0.6;

    &:hover {
      filter: grayscale(0);
      opacity: 1;
    }
  }
}
</style>
