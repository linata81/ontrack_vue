<script setup>
import BaseSelect from './BaseSelect.vue';

const props = defineProps({
  timelineItem: {
    required: true,
    type: Object
  }
})

const hourLinkClasses = [
  'absolute -top-4 left-1/2 rounded px-2 font-mono text-lg -translate-x-1/2',
  props.timelineItem.hour === new Date().getHours()
  ? 'bg-purple-900 font-black text-white'
  : 'bg-gray-100 text-gray-500'
]

const options = [
  {value: 1, label: 'Программирование'},
  {value: 2, label: 'Чтение'},
  {value: 3, label: 'Тренировка'}
]

const selectedActivityId = 2
</script>

<template>
  <li class="relative flex flex-col gap-2 border-t border-gray-200 py-10 px-4">
    <a href="#" :class="hourLinkClasses"> {{ timelineItem.hour }}:00 </a>
    <BaseSelect :selected="selectedActivityId" :options="options" placeholder="Отдых"/>
  </li>
</template>