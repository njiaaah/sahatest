<script setup lang="ts">
import { ref } from 'vue'
import ModalButton from './ModalButton.vue'
import FolderItem from './FolderItem.vue'

const props = defineProps<{
  title?: string
  isOpen?: boolean
  data?: Array<{ id: number; [key: string]: string }>
}>()

const emit = defineEmits<{
  (event: 'close'): void
  (event: 'log', folderId: number | null): void
}>()

const selectedFolder = ref<number | null>(null)

function closeModal() {
  emit('close')
}

function getFolderId(id: number) {
  if (selectedFolder.value == id) {
    selectedFolder.value = null
  } else {
    selectedFolder.value = id
  }
}

function handleOk() {
  emit('close')
  emit('log', selectedFolder.value)
  selectedFolder.value = null
}
</script>

<template>
  <div v-if="props.isOpen" class="fixed w-screen h-screen left-0 top-0 grid items-center">
    <!-- backdrop -->
    <div @click="closeModal" class="w-full h-full absolute bg-black opacity-25"></div>
    <!-- modal itself -->
    <div class="bg-white z-10 w-1/2 mx-auto p-4 rounded-xl flex flex-col">
      <h4 class="font-bold font-xl">{{ props.title || 'Title is missing' }}</h4>
      <!-- folders -->
      <ul class="flex flex-col gap-2 my-10 p-2 h-fit ml-4 max-h-[500px] overflow-y-auto">
        <FolderItem
          @get-folder-id="getFolderId"
          v-for="item in props.data || []"
          :key="item.id"
          v-bind="item"
          :isSelected="item.id === selectedFolder"
          :selectedFolder="selectedFolder"
        />
      </ul>
      <!-- button -->
      <div class="flex justify-between h-fit">
        <ModalButton class="px-16" @click="handleOk" color="red" title="Ok" />
        <ModalButton class="px-16" @click="closeModal" color="gray" title="Close" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
