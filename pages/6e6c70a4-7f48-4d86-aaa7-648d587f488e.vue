<template>
    <TresDirectionalLight ref="light"></TresDirectionalLight>
</template>
<script setup lang="js">
import { useTemplateRef, onMounted, getCurrentInstance } from "vue";
import { useTresContext, useRenderLoop } from "@tresjs/core";
//import { DirectionalLightHelper } from "three";

const { appContext: { app: { config: { globalProperties } } } } = getCurrentInstance(),
    { scene, camera } = useTresContext(),
    { onLoop } = useRenderLoop(),
    light = useTemplateRef("light");

onMounted(() => {
    //const dirlightHelper = new DirectionalLightHelper(light.value);
    //scene.value.add(dirlightHelper);
    scene.value.add(light.value.target);
});

onLoop(() => {
    const { is180, is90, cos, sin, angle } = globalProperties;
    if (is180) light.value.intensity = 0;
    else light.value.intensity = (180 * is90 + Math.sign(cos) * angle) / 90;
    light.value.target.position.copy(camera.value.position);
    //light.value.target.position.y = light.value.target.position.y - 1;
    light.value.position.set(light.value.target.position.x, (camera.value.far + light.value.target.position.y) * sin, - (camera.value.far + light.value.target.position.z) * cos)
    //dirlightHelper.update();
});

</script>