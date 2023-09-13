<template>
  <div>
    <div class="mt-1 rounded-md w-full">
      <div class="flex w-full items-center">
        <div class="relative flex w-full pr-1">
          <input
              type="text"
              name="text" id="text"
              class="block w-full shadow-sm rounded-md border-0 py-1 pr-2 ring-1 ring-inset placeholder:text-dark-300 focus:ring-2 focus:ring-inset sm:text-sm sm:leading-6"
              placeholder="Do the dishes"
              :class="{'ring-indigo-300 focus:ring-indigo-300 text-dark-500': newTask.length >= 4  || !errorInput, 'ring-red-300 focus:ring-red-500 text-red-900': newTask.length < 4 && errorInput}"
              v-model="newTask"
              aria-invalid="true"
              aria-describedby="text-error"
              @change="() => console.log(newTask)"
              @keydown.enter="addTask"
          />
          <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-3" :class="{'hidden': newTask.length >= 4  || !errorInput}">
            <ExclamationCircleIcon class="h-2 w-2 text-red-500" aria-hidden="true" />
          </div>
        </div>
        <button
            type="button"
            @click="addTask"
            class="rounded-lg mr-2 bg-indigo-600 px-2 h-5 text-sm font-semibold sm:font-normal text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 whitespace-nowrap">
          Create
        </button>
        <TodoCommands
            v-on:massChecking="checkOrUncheckAll"
            v-on:deletingAll="emit('deletingAll')"
        />
      </div>
    </div>
    <p class="mt-1 text-sm text-red-600" :class="{'hidden': newTask.length >= 4 || !errorInput}" id="text-error">The task name has to be at least 4 characters long</p>
  </div>
</template>

<script setup lang="ts">
import { ExclamationCircleIcon } from '@heroicons/vue/20/solid'
import {ref} from "vue";
import TodoCommands from "./TodoCommands.vue";
const newTask = ref('');
const errorInput = ref(false);
const emit = defineEmits<{
  (e: 'creating', title: string): void
  (e: 'massChecking', action: 'check' | 'uncheck'): void
  (e: 'deletingAll'): void
}>()
const addTask = () => {
  if (newTask.value.length < 4) {
    errorInput.value = true
    return
  }
  emit('creating', newTask.value)
  errorInput.value = false
  newTask.value = ''
}
const checkOrUncheckAll = (action: 'check' | 'uncheck') => emit('massChecking', action)

</script>