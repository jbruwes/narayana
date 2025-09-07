<template>
    <TresFog ref="fogRef" :args="[0, 10, 200]"></TresFog>
</template>
<script setup lang="ts">
import { useTemplateRef, onMounted } from 'vue';
import { useRenderLoop } from '@tresjs/core';

const { onLoop } = useRenderLoop(),
    fog = useTemplateRef("fogRef");

onMounted(() => {
    onLoop(({ elapsed }) => {
        const day = Math.trunc(elapsed / 360),
            isNight = Math.trunc(elapsed / 180) % 2,
            angle = elapsed - 360 * day,
            isQuater = Math.trunc(angle / 90) % 2,
            radian = angle * Math.PI / 180,
            cos = Math.cos(radian);

        if (isNight) fog.value.color.setRGB(0, 0, 0);
        else fog.value.color.setHSL(0.5, 0.92, 0.5 * (180 * isQuater + Math.sign(cos) * angle) / 90);
    });
});
</script>