<script setup lang="ts">
import { XMarkIcon} from "@heroicons/vue/20/solid";

defineProps({
  id: Number,
  title: String,
  completed: Boolean,
  className: String
})
const emit = defineEmits<{
  (e: 'checking', id: number): void
  (e: 'deleting', id: number): void
}>()
</script>

<template>
  <div class="relative flex items-center w-full" v-bind:class="className">
    <div class="flex items-center grow pr-4">
      <div class="flex h-6 items-center">
        <input
            v-bind:checked="completed"
            id="offers"
            aria-describedby="Task description"
            name="offers"
            type="checkbox"
            @change="emit('checking', id)"
            class="h-3 w-3 rounded-lg border-gray-300 text-indigo-600 focus:ring-indigo-600" />
      </div>
      <div class="ml-3 text-sm leading-6">
        <label for="offers" :class="completed ? 'text-gray-400 font-normal' : 'text-gray-900 font-medium'">{{title}}</label>
      </div>
    </div>

    <button type="button" class="bg-red-100 group w-4 h-4 rounded-full hover:bg-red-200 flex justify-center items-center" @click="emit('deleting', id)">
      <XMarkIcon class="text-red-800 h-3 w-3 group-hover:text-red-900" />
    </button>
  </div>
</template>