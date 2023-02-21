<script setup>
import { ref, computed } from 'vue';

const duration = ref(false);
const rank = computed(() => {
  if (duration.value) {
    let result;
    if (duration.value <= 250)
      result = 'perfect'
    else if (duration.value <= 500)
      result = 'rapid reflexes'
    else
      result = ['naah man', 'pffff', 'improvable'][Math.floor(Math.random() * 3)]

    return result
  }
})

const props = defineProps({ delay: Number })
defineEmits(['restart'])

await new Promise(resolve => setTimeout(resolve, props.delay))
const begin = Date.now();

function handleClick() {
  duration.value = Date.now() - begin
}
</script>

<template>
  <div @click="!duration && handleClick()" class="w-96 h-60 rounded-3xl text-2xl bg-cyan-500 mt-5 mx-auto flex items-center justify-center">
    click
  </div>
  <div v-if="duration" class="mt-5">
    <span class="text-lg">{{ duration }} ms</span>
    <div class="text-xl font-bold mt-2 text-teal-500">{{ rank }}</div>
    <button @click="$emit('restart')" class="bg-sky-500">restart</button>
  </div>
</template>
