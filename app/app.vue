<script setup lang="ts">
import { OrbitControls } from 'three/addons/controls/OrbitControls'
import { extend } from '@tresjs/core'
import { SRGBColorSpace } from 'three'

extend({ OrbitControls })
</script>

<template>
  <main :style="{ width: '100vw', height: '100vh' }">
    <div class="grain-filter" />

    <svg class="absolute inset-0">
      <filter id="noiseFilter">
        <feTurbulence
          type="fractalNoise"
          baseFrequency="0.7"
        />
        <feComposite
          operator="in"
          in2="SourceGraphic"
          result="monoNoise"
        />
      </filter>
    </svg>

    <TresCanvas
      window-size
      :output-color-space="SRGBColorSpace"
      class="canvas"
    >
      <TheCamera />
      <!-- <TresAxesHelper /> -->

      <TheNoise />
    </TresCanvas>
  </main>
</template>

<style>
body, html {
  margin: 0;
  background: black;
}

.grain-filter {
  filter: url(#noiseFilter);
  background: black;
  position: fixed;
  inset: 0;
  z-index: 50;
  opacity: 0.25;
}

.canvas {
  opacity: 0.75;
}
</style>
