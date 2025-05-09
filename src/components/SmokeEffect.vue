<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'

const smoke = ref<HTMLCanvasElement | null>(null)

onMounted(() => {
  generateSmoke()
})

onUnmounted(() => {})

function generateSmoke() {
  if (!smoke.value) {
    return
  }

  const NUM_PARTICLES = 50
  const canvas = smoke.value
  const ctx = canvas.getContext('2d') as CanvasRenderingContext2D
  let raf: number

  if (canvas) {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight + 100
  }

  const particles: Particle[] = []
  const fps = 60
  const fpsInterval = 1000 / fps
  let then = Date.now()

  // Carga la textura de humo
  const smokeImage = new Image()
  smokeImage.src = new URL('../assets/images/smoke.webp', import.meta.url).href

  class Particle {
    x: number
    y: number
    size: number
    opacity: number
    rotation: number
    rotationSpeed: number

    constructor() {
      this.x = Math.random() * canvas.width - canvas.width
      this.y = Math.random() * canvas.height - canvas.height / 2
      this.size = Math.random() * 3000 + 1000 // Ajustar para textura y 'z'
      this.opacity = Math.random() * 0.8 // Opacidad inicial aleatoria
      this.rotation = Math.random() * Math.PI * 2 // Rotación inicial aleatoria
      this.rotationSpeed = Math.random() * 0.002 // Velocidad de rotación
    }

    update() {
      this.rotation += this.rotationSpeed // Actualizar la rotación
    }

    draw() {
      ctx.save() // Guardar el estado actual del contexto
      ctx.translate(this.x + this.size / 2, this.y + this.size / 2) // Mover el origen al centro de la partícula
      ctx.rotate(this.rotation) // Rotar
      ctx.globalAlpha = this.opacity // Opacidad
      ctx.drawImage(smokeImage, -this.size / 2, -this.size / 2, this.size, this.size) // Dibujar imagen
      ctx.globalAlpha = 1.0 // Restablecer opacidad
      ctx.restore() // Restaurar el estado original del contexto
    }
  }

  function init() {
    for (let i = 0; i < NUM_PARTICLES; i++) {
      particles.push(new Particle())
    }
  }

  function handleParticles() {
    for (let i = 0; i < particles.length; i++) {
      particles[i].update()
      particles[i].draw()

      if (particles[i].size <= 1) {
        particles.splice(i, 1)
        i--
        particles.push(new Particle()) // Añadir nueva partícula para mantener el número
      }
    }
  }

  function animate() {
    raf = requestAnimationFrame(animate)

    const now = Date.now()
    const elapsed = now - then

    if (elapsed > fpsInterval) {
      then = now - (elapsed % fpsInterval)

      ctx.clearRect(0, 0, canvas.width, canvas.height)
      handleParticles()
    }
  }

  const reducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)')

  if (!reducedMotion.matches) {
    window.addEventListener('resize', () => {
      canvas.width = window.innerWidth
      canvas.height = window.innerHeight + 100
      cancelAnimationFrame(raf)
      handleParticles()
      animate()
    })

    smokeImage.onload = () => {
      init()
      animate()
    }
  }
}
</script>

<template>
  <div class="smoke">
    <canvas ref="smoke"></canvas>
  </div>
</template>

<style scoped>
.smoke {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;

  canvas {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
