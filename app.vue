<script setup lang="ts">
  // Component imports
  import AppHeader from "./components/AppHeader.vue"
  import AppCard from "./components/AppCard.vue"
  import AppMenu from "./components/AppMenu.vue"
  import AppEditButton from "./components/AppEditButton.vue"
  import AppApplyButton from "./components/AppApplyButton.vue"
  import AppCancelButton from "./components/AppCancelButton.vue"

</script>

<template>
  <AppHeader/>
  <div class="container">
    <AppCard/>
  </div>
</template>

<style scoped>
  .container {
    height: 500px;
    width: 100vw;
    background-color: white;
  }
</style>