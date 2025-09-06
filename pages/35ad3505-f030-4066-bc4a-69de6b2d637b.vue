<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :far="100"></TresPerspectiveCamera>
    <MapControls></MapControls>
    <RouterView></RouterView>
  </TresCanvas>
</template>

<script setup lang="js">
import { TresCanvas } from '@tresjs/core';
import { MapControls } from '@tresjs/cientos';


/*
*/
/*
const target = computed(()=>{
  console.log(camera.value?.position);

//  dirLight.target.position.copy(camera.position.);
//  dirLight.target.position.y=0;
//	dirLight.target.updateMatrixWorld();
  return camera.value?.position;
});
*/
//watch(camera, (value) => { console.log(value) });
</script>
