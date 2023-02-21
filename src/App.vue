<script setup>
import { ref } from 'vue';
import Block from './components/Block.vue'

const isPlaying = ref(false);
const delay = ref(null);

function start() {
  delay.value = 2000 + Math.random() * 5000;
  isPlaying.value = true;
}
</script>

<template>
  <div class="w-full mb-3">
    <h1 class="text-4xl">reaction timer</h1>
  </div>
  <button @click="start" class="disabled:bg-violet-500/30" :disabled="isPlaying">start</button>
  <Suspense>
    <Block v-if="isPlaying" :delay="delay" @restart="isPlaying = false" />
  </Suspense>
</template>

<style lang="postcss" scoped>
:global(button) {
  @apply w-20 h-8 rounded bg-violet-500 mt-5 mb-5;
}
</style>
