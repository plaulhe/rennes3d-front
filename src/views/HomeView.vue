<script setup lang="ts">
// import HelloWorld from '../components/HelloWorld.vue'
import NetworkFigures from '../components/home/NetworkFigures.vue'
import MapComponent from '../components/map/MapComponent.vue'
// import LineDescriptions from '../components/home/LineDescriptions.vue'
// import TravelTimes from '../components/home/TravelTimes.vue'
</script>

<template>
  <main class="h-screen flex">
    <div class="w-72 p-4 bg-blue-300">
      <div class="">
        <NetworkFigures></NetworkFigures>
      </div>
    </div>
    <div class="flex grow relative">
      <!-- <HelloWorld msg="The home" /> -->
      <MapComponent></MapComponent>
      <!-- <div><TravelTimes></TravelTimes></div>
      <div><LineDescriptions></LineDescriptions></div> -->
    </div>
  </main>
</template>
