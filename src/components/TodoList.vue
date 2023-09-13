<script setup lang="ts">
import TodoCard from "./todo_card/TodoCard.vue";
import { ref, onMounted, watch } from 'vue';
import TodoInput from "./todo_input/TodoInput.vue";
import EmptyTodo from "./empty_todo/EmptyTodo.vue";

let todos = ref([]);

// Function to load tasks from local storage
const loadTasksFromLocalStorage = () => {
  const storedTasks = localStorage.getItem('tasks');
  if (storedTasks) {
    todos.value = JSON.parse(storedTasks);
  }
};

onMounted(() => {
  // Load tasks from local storage when the component is created
  loadTasksFromLocalStorage();
});

const onCheckboxChange = (id: number) => {
  const todo = todos.value.find(todo => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

const deleteTodo = (id: number) => {
  console.log('before', todos.value);
  todos.value = todos.value.filter(todo => todo.id !== id);
  console.log('after', todos.value);
  // Save tasks to local storage after deletion
  saveTasksToLocalStorage();
};

const addTodo = (title: string) => {
  todos.value.push({
    id: todos.value.length + 1,
    title,
    completed: false
  });
  // Save tasks to local storage after addition
  saveTasksToLocalStorage();
};

const checkOrUncheckAll = (action: 'check' | 'uncheck') => {
  todos.value.forEach(todo => (todo.completed = action === 'check'));
  // Save tasks to local storage after mass checking/unchecking
  saveTasksToLocalStorage();
};

const deleteAll = () => {
  todos.value = [];
  // Save tasks to local storage after deletion
  saveTasksToLocalStorage();
};

// Function to save tasks to local storage
const saveTasksToLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(todos.value));
};
</script>

<template>
  <div class="flex flex-col w-full h-full px-4 sm:px-10">
    <TodoInput
        v-on:creating="addTodo"
        v-on:massChecking="checkOrUncheckAll"
        v-on:deletingAll="deleteAll"
    />
    <span class="w-full h-[2px] my-2 bg-gray-200 rounded-full" />
  <fieldset class="h-full">
    <legend class="sr-only">Tasks list</legend>
    <TodoCard
        v-for="todo in todos"
        :key="todo.id"
        :id="todo.id"
        :title="todo.title"
        :completed="todo.completed"
        className="m-1"
        v-on:checking="onCheckboxChange"
        v-on:deleting="deleteTodo"
    />
    <EmptyTodo v-if="todos.length === 0" />
  </fieldset>
  </div>
</template>
