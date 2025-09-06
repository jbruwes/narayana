<template>
    <Stats></Stats>

    <Sky></Sky>
    <Grid :infinite-grid="true"></Grid>
    <TresAmbientLight></TresAmbientLight>
    <TresDirectionalLight ref="lightRef"
        :position="[0, 100 * Math.sin(0.6 * Math.PI / 180), -100 * Math.cos(0.6 * Math.PI / 180)]">
    </TresDirectionalLight>
</template>
<script setup lang="js">
import { useTemplateRef, onMounted } from 'vue';
import { Grid, Sky, Stats } from '@tresjs/cientos';
import { vLightHelper, useTresContext, useRenderLoop } from '@tresjs/core';
import { DirectionalLightHelper } from "three";

const { scene, camera } = useTresContext();
const { onLoop } = useRenderLoop();
const dirLight = useTemplateRef("lightRef");
onMounted(() => {
    const dirlightHelper = new DirectionalLightHelper(dirLight.value, 1);
    scene.value.add(dirlightHelper);
    scene.value.add(dirLight.value.target);
    onLoop(() => {
        dirLight.value.target.position.copy(camera.value.position);
        dirLight.value.target.position.y = 0;
        dirlightHelper.update();
    });
});
</script>