<script setup lang="ts">
import { ref } from 'vue'
import FolderMinus from './icons/FolderMinus.vue'
import FolderPlus from './icons/FolderPlus.vue'
import FolderEmpty from './icons/FolderEmpty.vue'

const props = defineProps<{
  name?: string
  children?: Array<{ id: number; [key: string]: string }>
  id?: number
  isSelected?: boolean
  selectedFolder?: number | null
}>()

const emit = defineEmits<{
  (event: 'get-folder-id', id: number): void
}>()

const isFolderOpen = ref(false)

function selectFolder() {
  emit('get-folder-id', props.id || 0)
}
</script>

<template>
  <div>
    <div
      class="ring-1 ring-gray-200 bg-gray-50 rounded-xl w-fit flex gap-4 items-center cursor-pointer"
      :class="{ selected: props.isSelected }"
    >
      <!-- icon -->
      <div v-if="props.children.length === 0" class="p-2 grid items-center">
        <FolderEmpty />
      </div>
      <div
        v-else
        @click="isFolderOpen = !isFolderOpen"
        class="p-2 hover:bg-gray-300 cursor-pointer rounded-full grid items-center"
      >
        <FolderMinus v-if="isFolderOpen" />
        <FolderPlus v-else />
      </div>
      <!-- title -->
      <span @click="selectFolder" class="p-1 pr-5 select-none">
        {{ props.name }}
        <span>({{ props.children.length }})</span>
      </span>
    </div>
    <div
      v-if="isFolderOpen"
      class="flex flex-col gap-2 ml-8"
      :class="{ 'mb-6 ': props.children.length > 0, 'mt-4': props.children.length > 0 }"
    >
      <FolderItem
        v-for="item in props.children"
        :key="item.id"
        v-bind="item"
        @get-folder-id="emit('get-folder-id', $event)"
        :isSelected="item.id === props.selectedFolder"
        :selectedFolder="props.selectedFolder"
      />
    </div>
  </div>
</template>

<style scoped>
.selected {
  background-color: #ccc;
  outline: 1px solid #ff1b1b;
}
</style>
