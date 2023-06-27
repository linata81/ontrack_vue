<script setup>
import {PAGE_TIMELINE, PAGE_ACTIVITIES, PAGE_PROGRESS} from '../constants.js'
import NavItem from './NavItem.vue'
import { ClockIcon, ListBulletIcon, ChartBarIcon } from '@heroicons/vue/24/outline'

defineProps(['currentPage'])

const emit = defineEmits(['navigate'])

const navItems = {
  // определяем ключи на основе динамических значений с помощью []
  [PAGE_TIMELINE]: ClockIcon,
  [PAGE_ACTIVITIES]: ListBulletIcon,
  [PAGE_PROGRESS]: ChartBarIcon
}
</script>

<template>
  <nav class="sticky bottom-0 z-10 bg-white">
    <ul class="flex items-center justify-around border-t">
      <NavItem
        v-for="icon, page in navItems"
        :key="page"
        :href="`#${page}`"
        :class="{'bg-gray-200 pointer-events-none': page === currentPage}"
        @click="emit('navigate', page)"
      >
        <component :is="icon" class="h-6 w-6"/> {{ page }}
      </NavItem>
    </ul>
  </nav>
</template>