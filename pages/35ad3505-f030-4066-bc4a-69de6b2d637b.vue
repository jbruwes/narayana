<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera></TresPerspectiveCamera>
    <router-view></router-view>
  </TresCanvas>
</template>

<script lang="js" setup>
import { TresCanvas } from '@tresjs/core';
</script>
