<template>
    <Suspense>
        <EffectComposerPmndrs>
            <FXAAPmndrs></FXAAPmndrs>
            <BloomPmndrs mipmap-blur></BloomPmndrs>
        </EffectComposerPmndrs>
    </Suspense>
</template>
<script setup lang="js">
import { EffectComposerPmndrs, FXAAPmndrs, BloomPmndrs } from '@tresjs/post-processing';
</script>