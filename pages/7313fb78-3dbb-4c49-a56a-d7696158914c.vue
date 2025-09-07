<template>
    <OrbitControls :target="[0, 3, -1]"></OrbitControls>
</template>
<script setup lang="js">
import { OrbitControls } from '@tresjs/cientos';
</script>