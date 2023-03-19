<script setup lang="ts">
import type { Task } from "~~/types";
import { nanoid } from "nanoid";

const emit = defineEmits<{
  (e: "add", payload: Task): void;
}>();

const focused = ref(false);
const title = ref("");

const createTask = (e: Event) => {
  if (title.value.trim()) {
    e.preventDefault();
    emit("add", {
      title: title.value.trim(),
      createdAt: new Date(),
      id: nanoid(),
    });
  }
  title.value = "";
};
</script>

<template>
  <div>
    <textarea
      v-model="title"
      @keydown.tab="createTask"
      @keyup.enter="createTask"
      class="focus:bg-white focus:shadow resize-none rounded w-full border-none px-2 py-2 bg-gray-200 cursor-pointer"
      :class="{
        'h-7': !focused,
        'h-20': focused,
      }"
      style="outline: none !important"
      @focus="focused = true"
      @blur="focused = false"
      :placeholder="!focused ? '+ Add A Card' : 'Enter a title for this card'"
    />
  </div>
</template>
