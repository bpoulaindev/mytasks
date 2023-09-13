<script setup>
import TodoList from "./components/TodoList.vue";
</script>

<template>
  <div class="flex w-full h-[calc(100dvh)] sm:justify-center items-center bg-cream sm:px-16 flex-col">
    <div class="flex items-center sm:mt-10 sm:mb-4">
      <img src="./assets/mytasks.svg" alt="MyTasks" class="h-4 w-4 mr-1" />
      <h1 class="text-3xl font-bold text-gray-900">MyTasks</h1>
    </div>
    <TodoList />
  </div>
</template>
