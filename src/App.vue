<script setup>
import {PAGE_TIMELINE, PAGE_ACTIVITIES, PAGE_PROGRESS} from './constants.js'
import {ref} from 'vue'
import TheHeader from './components/TheHeader.vue'
import TheNav from './components/TheNav.vue';
import TheTimeline from './pages/TheTimeline.vue';
import TheActivities from './pages/TheActivities.vue';
import TheProgress from './pages/TheProgress.vue';
import {normalizePageHash} from './functions'

// делаем чтобы значение тек. стр-цы соответствовало значению хэша в адресной строке
const currentPage = ref(normalizePageHash())

function goTo(page) {
  currentPage.value = page
}
</script>

<template>
  <div class="container lg mx-auto flex flex-col min-h-screen">

    <TheHeader
      @go-to-timeline="goTo(PAGE_TIMELINE)"
      @go-to-progress="goTo(PAGE_PROGRESS)"
    />

    <main class="flex flex-grow flex-col">
      <TheTimeline v-show="currentPage === PAGE_TIMELINE"/>
      <TheActivities v-show="currentPage === PAGE_ACTIVITIES"/>
      <TheProgress v-show="currentPage === PAGE_PROGRESS"/>
    </main>

    <TheNav :current-page="currentPage" @navigate="goTo($event)"/>
  </div>
</template>

<style scoped></style>