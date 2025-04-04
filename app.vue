<script setup lang="ts">
  // Component imports
  import AppHeader from "./components/AppHeader.vue"
  import AppCard from "./components/AppCard.vue"
  import AppMenu from "./components/AppMenu.vue"

  import { ref } from "vue";
  const isMenuVisible = ref(false);

  const toggleMenu = () => {
    isMenuVisible.value = !isMenuVisible.value;
    console.log(isMenuVisible.value);
  };
</script>

<template>
  <AppMenu v-if="isMenuVisible" @toggle-menu="toggleMenu"/>
  <AppHeader/>
  <div class="container">
    <AppCard @toggle-menu="toggleMenu" />
    <AppCard @toggle-menu="toggleMenu" />
    <AppCard @toggle-menu="toggleMenu" />
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