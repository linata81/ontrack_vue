<script setup>
import {PAGE_TIMELINE, PAGE_ACTIVITIES, PAGE_PROGRESS} from './constants.js'
import {ref} from 'vue'
import TheHeader from './components/TheHeader.vue'
import TheNav from './components/TheNav.vue';
import TheTimeline from './pages/TheTimeline.vue';
import TheActivities from './pages/TheActivities.vue';
import TheProgress from './pages/TheProgress.vue';

// делаем чтобы значение тек. стр-цы соответствовало значению хэша в адресной строке
const currentPage = ref(normalizePageHash())

function normalizePageHash() {
  const hash = window.location.hash.slice(1)
  
  if([PAGE_TIMELINE, PAGE_ACTIVITIES, PAGE_PROGRESS].includes(hash)) {
    return hash
  }
  
  window.location.hash = PAGE_TIMELINE
  return PAGE_TIMELINE  
}

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