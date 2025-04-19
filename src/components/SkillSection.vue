<script setup lang="ts">
import { ref, onMounted } from 'vue'

const pVideo = new URL('../assets/vids/p.mp4', import.meta.url).href
const qVideo = new URL('../assets/vids/q.mp4', import.meta.url).href
const wVideo = new URL('../assets/vids/w.mp4', import.meta.url).href
const eVideo = new URL('../assets/vids/e.mp4', import.meta.url).href
const rVideo = new URL('../assets/vids/r.mp4', import.meta.url).href

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
  <h2 ref="h2" :class="{ animate: isVisible }">Skills</h2>
  <section id="abilities" class="section">
    <div class="card">
      <div class="text">
        <h3>[Pasiva] Llamada del viajero</h3>
        <p>
          Debo ir por el mapa recogiendo mis meeps. Me dan velocidad de movimiento, experiencia,
          maná, y pontenciarán mis básicos. Por lo que tendrás que estar pendiente para retroceder a
          la torre cuando estés solo. Volveré rápidamente con mi <span>periplo mágico</span>
        </p>
      </div>
      <div class="video">
        <video loop controls>
          <source :src="pVideo" type="video/mp4" />
        </video>
      </div>
    </div>
    <div class="card">
      <div class="text">
        <h3>[Q] Cadenas Cósmicas</h3>
        <p>
          Con mi Q stuneo a campeones siempre y cuando choquen con algo detrás, ya sea un minion,
          una pared, estructura u otro campeón. El stun dura aproximadamanete 1-2 segundos, así que
          deberás aprovechar este momento para pokear.
        </p>
      </div>
      <div class="video">
        <video loop controls>
          <source :src="qVideo" type="video/mp4" />
        </video>
      </div>
    </div>
    <div class="card">
      <div class="text">
        <h3>[W] Santuario del Protector</h3>
        <p>
          Mi W cura. Las iré poniendo en el camino para tener sustain en línea. Además de curarte te
          da velocidad de movimiento, así que trata de usarlas cuando necesites velocidad (por
          ejemplo escapando del enemigo). IMPORTANTE: La cura se carga (3 segundos), espera que esté
          completamente cargada para recibr la mayor cantidad de vida posible.
        </p>
      </div>
      <div class="video">
        <video loop controls>
          <source :src="wVideo" type="video/mp4" />
        </video>
      </div>
    </div>
    <div class="card">
      <div class="text">
        <h3>[E] Periplo Mágico</h3>
        <p>
          Este es mi portal. El equipo viajará más rápido que el enemigo. Lo usaré mucho en conjunto
          con el jungla para hacer gankeos sorpresas tanto en bot como en jungla. También abriré
          portales en teamfights para salir rápido si es necesario.
        </p>
      </div>
      <div class="video">
        <video loop controls>
          <source :src="eVideo" type="video/mp4" />
        </video>
      </div>
    </div>
    <div class="card">
      <div class="text">
        <h3>[R] Destino Maleable</h3>
        <p>
          Mi R es un Zonyhas en área y afecta a todos por igual. Trataré siempre de darle solo al
          enemigo, así que trata de evadirla cuando veas la marca. Mientras mas lejos la lance de
          mí, mas se va a tardar en llegar la R.
        </p>
      </div>
      <div class="video">
        <video loop controls>
          <source :src="rVideo" type="video/mp4" />
        </video>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section {
  width: 90%;
  max-width: 900px;
  margin-top: 4rem;
}

h2 {
  opacity: 0;
}

h2.animate {
  animation: fadeIn 2s ease-in-out forwards;
}

.card {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 2rem;
  padding: 1rem;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 1rem;

  h3 {
    font-size: 1.5rem;
    font-weight: bold;
    color: white;
    margin-bottom: 1rem;
  }

  .text,
  .video {
    flex: 1;
  }

  .text {
    line-height: 1.5;
    font-size: 1.1rem;
  }

  &:nth-child(even) {
    flex-direction: row-reverse;
  }
}

video {
  width: 100%;
  border-radius: 1rem;
}
</style>
