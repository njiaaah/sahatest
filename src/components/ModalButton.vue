<script setup lang="ts">
const props = defineProps({
  title: { type: String, default: 'Button' },
  color: { type: String, default: 'sky' },
})

const color = 'bg-' + props.color + '-500'

const emit = defineEmits(['click'])

const onClick = () => {
  emit('click')
}
</script>

<template>
  <button
    class="font-bold outline px-4 py-2 rounded-full outline-1 hover:scale-105 active:scale-90 transition-transform text-white"
    :class="[color]"
    @click="onClick"
  >
    {{ props.title }}
  </button>
</template>

<style scoped></style>
