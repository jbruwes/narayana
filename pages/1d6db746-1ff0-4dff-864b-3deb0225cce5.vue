<template>
    <TresFog ref="fogRef" :args="[0, camera.near, camera.far/10]"></TresFog>
</template>
<script setup lang="ts">
import { useTemplateRef, getCurrentInstance } from "vue";
import { useRenderLoop, useTresContext } from "@tresjs/core";

const { appContext: { app: { config: { globalProperties } } } } = getCurrentInstance(),
    { onLoop } = useRenderLoop(),
    { camera } = useTresContext(),
    fog = useTemplateRef("fogRef");


onLoop(() => {
    const { is180, is90, cos, angle } = globalProperties;
    if (is180) fog.value.color.setRGB(0, 0, 0);
    else fog.value.color.setHSL(0.5, 0.92, 0.5 * (180 * is90 + Math.sign(cos) * angle) / 90);
});

</script>