<script setup lang="ts">
import draggable from "vuedraggable";
import type { Column, Task } from "../types/index";
import { nanoid } from "nanoid";

const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: "Backlog",
    tasks: [
      {
        id: nanoid(),
        title: "Create marketing loading page",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Develop cool new feature",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Fix page nav bug",
        createdAt: new Date(),
      },
    ],
  },
  {
    id: nanoid(),
    title: "Selected for Dev",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "In progress",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "QA",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Complete",
    tasks: [],
  },
]);
</script>

<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      class="flex gap-4 overflow-x-auto items-start"
      ghost-class="opacity-30"
      :animation="150"
      handle=".drag-handle"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="bg-gray-200 column p-5 rounded min-w-[250px]">
          <header class="font-bold mb-4">
            <DragHandler />
            {{ column.title }}
          </header>
          <draggable
            v-model="column.tasks"
            group="tasks"
            item-key="id"
            handle=".drag-handle"
            ghost-class="opacity-30"
            :animation="150"
          >
            <template #item="{ element: task }: { element: Task }">
              <BoardTask :task="task" />
            </template>
          </draggable>
          <footer>
            <button class="text-gray-500">+ Add a Card</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
