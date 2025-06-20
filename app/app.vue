<script setup lang="ts">
import { OrbitControls } from 'three/addons/controls/OrbitControls'
import { extend } from '@tresjs/core'
import { SRGBColorSpace } from 'three'

extend({ OrbitControls })
</script>

<template>
  <div>
    <TresCanvas
      window-size
      :output-color-space="SRGBColorSpace"
    >
      <!-- <TresOrthographicCamera
        :position="[0, 0, 1]"
      /> -->
      <TresPerspectiveCamera
        :position="[0, -1, 0.8]"
        :look-at="[0, 0, -0.8]"
      />

      <!-- <TheOrbitControls /> -->
      <TresAxesHelper />

      <TheNoise />
    </TresCanvas>
  </div>
</template>
