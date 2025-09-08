<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 3, 0]" ref="camera" :far="1000"></TresPerspectiveCamera>
    <RouterView></RouterView>
  </TresCanvas>
</template>

<script setup lang="js">
import { getCurrentInstance } from "vue";
import { TresCanvas, useRenderLoop } from "@tresjs/core";

const { appContext: { app: { config: { globalProperties } } } } = getCurrentInstance(),
  { onLoop } = useRenderLoop();

onLoop(({ elapsed }) => {
  globalProperties.angle = elapsed - 360 * Math.trunc(elapsed / 360);
  globalProperties.is180 = Math.trunc(globalProperties.angle / 180) % 2;
  globalProperties.is90 = Math.trunc(globalProperties.angle / 90) % 2;
  const radian = globalProperties.angle * Math.PI / 180;
  globalProperties.sin = Math.sin(radian);
  globalProperties.cos = Math.cos(radian);
});

</script>
