<script setup lang="ts">
import { Color, DoubleSide, Vector2 } from 'three'
import commonVertex from '~/shader/vertex.glsl?raw'
import noiseFrag from '~/shader/noise.glsl?raw'

const width = ref(window.innerWidth)
const height = ref(window.innerHeight)

const palette = ['#f2766b', '#586166', '#081b26']
const colors = palette.map(color => new Color(color))

const { onLoop } = useRenderLoop()

const uniforms = {
  resolution: { value: new Vector2(width.value, height.value) },
  colors: { value: colors },
  time: { value: 0 },
}

onLoop(({ elapsed }) => {
  uniforms.time.value = elapsed
})

onMounted(() => {
  window.addEventListener('resize', () => {
    const val = uniforms.resolution.value as Vector2

    const w = window.innerWidth
    const h = window.innerHeight

    val.set(w, h)
    width.value = w
    height.value = h
  })
})
</script>

<template>
  <TresMesh>
    <TresPlaneGeometry
      :args="[1.5, 1.5, 300, 300]"
    />
    <!-- <TresPlaneGeometry :args="[width, height]" /> -->

    <TresShaderMaterial
      :vertex-shader="commonVertex"
      :fragment-shader="noiseFrag"
      :uniforms="uniforms"
      :side="DoubleSide"
    />
  </TresMesh>
</template>
