<script setup lang="ts">
import FolderModal from './components/FolderModal.vue'
import ModalButton from './components/ModalButton.vue'
import { ref } from 'vue'

const isModalOpen = ref(false)

interface Folder {
  id: number
  name: string
  children: Folder[]
}

const mockFolders: Folder[] = [
  {
    id: 1,
    name: 'Млекопитающие',
    children: [
      { id: 2, name: 'Пауки-рыболовы', children: [] },
      {
        id: 3,
        name: 'Хищные',
        children: [
          {
            id: 4,
            name: 'Кошачьи',
            children: [
              { id: 6, name: 'Львинята', children: [] },
              {
                id: 7,
                name: 'Тигровые коты',
                children: [
                  { id: 8, name: 'Бенгальские тигры', children: [] },
                  { id: 9, name: 'Азиатские львята', children: [] },
                ],
              },
              {
                id: 10,
                name: 'Собачьи',
                children: [
                  { id: 11, name: 'Шар-Пеи', children: [] },
                  { id: 12, name: 'Волки', children: [] },
                ],
              },
            ],
          },
          {
            id: 13,
            name: 'Слоновые',
            children: [
              { id: 14, name: 'Африканские слоны', children: [] },
              { id: 15, name: 'Индийские слоны', children: [] },
            ],
          },
        ],
      },
    ],
  },
  {
    id: 5,
    name: 'Птицы',
    children: [
      { id: 16, name: 'Кулики', children: [] },
      {
        id: 17,
        name: 'Дятлы',
        children: [
          { id: 18, name: 'Обыкновенные дятлы', children: [] },
          { id: 19, name: 'Белолобые дятлы', children: [] },
        ],
      },
      {
        id: 20,
        name: 'Попугаи',
        children: [
          { id: 21, name: 'Амазонки', children: [] },
          { id: 22, name: 'Клинохвостые попугаи', children: [] },
        ],
      },
    ],
  },
  {
    id: 23,
    name: 'Рептилии',
    children: [
      {
        id: 24,
        name: 'Змеи',
        children: [
          { id: 25, name: 'Удововидные змеи', children: [] },
          { id: 26, name: 'Питоны', children: [] },
        ],
      },
      {
        id: 27,
        name: 'Червящиеся',
        children: [
          { id: 28, name: 'Крокодилы', children: [] },
          { id: 29, name: 'Алигаторы', children: [] },
        ],
      },
    ],
  },
]
</script>

<template>
  <main>
    <ModalButton @click="isModalOpen = true" :title="'Открыть'" />

    <FolderModal
      :is-open="isModalOpen"
      @close="isModalOpen = false"
      @log="console.log('Идентификатор выбранной папки - ', $event)"
      :title="'Текст заголовка модального окна'"
      :data="mockFolders"
    />
  </main>
</template>

<style scoped></style>
