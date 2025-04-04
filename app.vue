<script setup lang="ts">
  // Component imports
  import AppHeader from "./components/AppHeader.vue"
  import AppCard from "./components/AppCard.vue"
  import AppMenu from "./components/AppMenu.vue"

</script>

<template>
  <AppMenu/>
  <AppHeader/>
  <div class="container">
    <AppCard/>
    <AppCard/>
    <AppCard/>
  </div>
</template>

<style scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
    background: radial-gradient(circle 370px at center, yellow -300%, #000 100%);
    position: absolute;
  }
</style>