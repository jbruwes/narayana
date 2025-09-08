<template>
    <TresMesh ref="sky">
        <SphereGeometry :args="[camera.far - 1]"></SphereGeometry>
        <TresMeshBasicMaterial :side="BackSide"></TresMeshBasicMaterial>
    </TresMesh>
</template>
<script setup lang="js">
import { BackSide } from "three";
import { useTresContext, useRenderLoop } from "@tresjs/core";
import { useTemplateRef } from "vue";

const { camera } = useTresContext(),
    { onLoop } = useRenderLoop(),
    sky = useTemplateRef("sky");

onLoop(() => {
    sky.value.position?.copy(camera.value.position);
});


</script>