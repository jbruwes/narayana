<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 3, 0]">
      <Sphere ref="planeRef" :args="[2100, 10, 10]" :position="[0, 0, 0]">
        <TresMeshBasicMaterial :side="BackSide"></TresMeshBasicMaterial>
      </Sphere>
    </TresPerspectiveCamera>
    <RouterView></RouterView>
  </TresCanvas>
</template>

<script setup lang="js">
import { TresCanvas } from '@tresjs/core';
import { Sphere } from '@tresjs/cientos';
import { BackSide } from 'three';
</script>
