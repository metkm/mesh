<script setup lang="ts">
import { OrbitControls } from 'three/addons/controls/OrbitControls'
import { extend } from '@tresjs/core'

extend({ OrbitControls })
</script>

<template>
  <div>
    <TresCanvas window-size>
      <!-- <TresOrthographicCamera
        :position="[0, 0, 1]"
      /> -->
      <TresPerspectiveCamera :position="[0, 0, 2]" />
      <TheOrbitControls />

      <TheNoise />
    </TresCanvas>
  </div>
</template>
