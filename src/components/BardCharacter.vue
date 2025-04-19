<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'

const SIZE = 1.5
const ANIMATION = 11
const bard = ref<HTMLElement | null>(null)

let scene: THREE.Scene
let camera: THREE.PerspectiveCamera
let renderer: THREE.WebGLRenderer
let mixer: THREE.AnimationMixer

onMounted(() => {
  setupThreeJsBard()
  window.addEventListener('resize', onWindowResize)
})

onUnmounted(() => {
  window.removeEventListener('resize', onWindowResize)
})

function setupThreeJsBard() {
  if (!bard.value) return

  // Scene setup
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true })
  renderer.setSize(bard.value.clientWidth, bard.value.clientHeight)
  bard.value.appendChild(renderer.domElement)

  // Lighting
  const ambientLight = new THREE.AmbientLight(0xffffff, 1)
  scene.add(ambientLight)

  // Model loading
  const loader = new GLTFLoader()
  loader.load(new URL('../assets/3d/bard.glb', import.meta.url).href, (gltf) => {
    scene.add(gltf.scene)
    mixer = new THREE.AnimationMixer(gltf.scene)
    mixer.clipAction(gltf.animations[ANIMATION]).play()

    gltf.scene.traverse((child) => {
      if (!(child instanceof THREE.Mesh)) {
        return
      }

      if (child.material) {
        child.material.needsUpdate = true
        child.material.metalness = 0
        child.material.roughness = 1
      }
    })
  })

  camera.position.set(1, SIZE, SIZE + 0.25)
  camera.lookAt(0, 1.35, 0)

  const directionalLight = new THREE.DirectionalLight(0xffffff, 2)
  directionalLight.position.set(SIZE, SIZE, SIZE)
  scene.add(directionalLight)

  // Animation loop
  const animate = () => {
    requestAnimationFrame(animate)
    if (mixer) mixer.update(0.004)
    renderer.render(scene, camera)
  }
  animate()
}

function onWindowResize() {
  if (!bard.value) return
  camera.aspect = bard.value.clientWidth / bard.value.clientHeight
  camera.updateProjectionMatrix()
  renderer.setSize(bard.value.clientWidth, bard.value.clientHeight)
}
</script>

<template>
  <div ref="bard" class="bard"></div>
</template>

<style scoped>
.bard {
  position: relative;
  width: 100%;
  height: 100%;
  z-index: 1;
  top: 0rem;
}
</style>
