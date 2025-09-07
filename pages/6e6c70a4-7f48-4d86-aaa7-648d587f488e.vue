<template>
    <TresDirectionalLight ref="lightRef" :intensity="intensity"></TresDirectionalLight>
</template>
<script setup lang="ts">
import { useTemplateRef, onMounted, ref } from 'vue';
import { useTresContext, useRenderLoop } from '@tresjs/core';
import { DirectionalLightHelper } from "three";

const { scene, camera } = useTresContext(),
    { onLoop } = useRenderLoop(),
    light = useTemplateRef("lightRef"),
    intensity = ref(1);

onMounted(() => {
    const dirlightHelper = new DirectionalLightHelper(light.value);
    scene.value.add(dirlightHelper);
    scene.value.add(light.value.target);
    onLoop(({ elapsed }) => {
        const day = Math.trunc(elapsed / 360),
            isNight = Math.trunc(elapsed / 180) % 2,
            angle = elapsed - 360 * day,
            quater = Math.trunc(angle / 90) % 2,
            radian = angle * Math.PI / 180,
            sin = Math.sin(radian),
            cos = Math.cos(radian);
        if (isNight) intensity.value = 0;
        else intensity.value = (180 * quater + Math.sign(cos) * angle) / 90;
        light.value.target.position.copy(camera.value.position);
        light.value.target.position.y = 0;
        light.value.position.set(light.value.target.position.x, camera.value.far * sin, (-camera.value.far + light.value.target.position.z) * cos)
        dirlightHelper.update();
    });
});
</script>