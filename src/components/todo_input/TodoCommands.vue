<template>
  <Menu as="div" class="relative inline-block text-left">
    <div>
      <MenuButton class="flex items-center rounded-full text-gray-400 hover:text-gray-600 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-100">
        <span class="sr-only">Open options</span>
        <EllipsisVerticalIcon class="h-3 w-3" aria-hidden="true" />
      </MenuButton>
    </div>

    <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
      <MenuItems class="absolute right-0 z-10 mt-2 w-40 origin-top-right rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none">
        <div class="py-1/2">
          <MenuItem v-slot="{ active }">
            <a href="#" :class="[active ? 'bg-indigo-50 text-indigo-800' : 'text-gray-700', 'block px-4 py-2 text-sm']" @click="emit('massChecking', 'check')">Check every task</a>
          </MenuItem>
          <MenuItem v-slot="{ active }">
            <a href="#" :class="[active ? 'bg-indigo-50 text-indigo-800' : 'text-gray-700', 'block px-4 py-2 text-sm']" @click="emit('massChecking', 'uncheck')">Uncheck every task</a>
          </MenuItem>
          <MenuItem v-slot="{ active }">
            <a href="#" :class="[active ? 'bg-indigo-50 text-indigo-800' : 'text-gray-700', 'block px-4 py-2 text-sm']" @click="emit('deletingAll')" >Delete all tasks</a>
          </MenuItem>
        </div>
      </MenuItems>
    </transition>
  </Menu>
</template>

<script setup lang="ts">
import { Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { EllipsisVerticalIcon } from '@heroicons/vue/20/solid'
const emit = defineEmits<{
  (e: 'massChecking', action: 'check' | 'uncheck'): void
  (e: 'deletingAll'): void
}>()
</script>