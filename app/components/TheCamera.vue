<script setup lang="ts">
import gsap from 'gsap'

const { camera } = useTresContext()

onMounted(() => {
  if (!camera.value) return

  const timeline = gsap.timeline()

  timeline.add('forward')
  timeline.add('back')

  timeline.to(
    camera.value.position,
    {
      duration: 0.5,
      z: 2,
      x: 2,
      delay: 1.0,
    },
    0,
  )

  const interpz = gsap.utils.interpolate(-0.8, 0)

  timeline.to(
    {},
    {
      duration: 0.5,
      delay: 1.0,
      onUpdate() {
        const z = interpz(this.ratio)
        camera.value?.lookAt(0, 0, z)
      },
    },
    0,
  )

  setTimeout(() => {
    console.log('reverse timeline')
    timeline.reverse(0)
  }, 3_000)
})
</script>

<template>
  <TresPerspectiveCamera
    :position="[0, -1, 0.8]"
    :look-at="[0, 0, -0.8]"
  />

  <!-- <TheOrbitControls
    v-if="renderer"
    :args="[camera, renderer?.domElement]"
  /> -->
</template>
