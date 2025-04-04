<script setup lang="ts">
  import AppButton from './AppButton.vue';

  import { defineEmits } from "vue";
  const emit = defineEmits(["toggle-menu"]);
</script>

<template>
  <div class="edit-menu-container">
    <div class="edit-menu">
      <div class="buttons-container">
        <AppButton @click="$emit('toggle-menu')" button-text="Apply" style="margin: 20px;"/>
        <AppButton @click="$emit('toggle-menu')" button-text="Cancel" style="margin: 20px"/>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .edit-menu-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
  position: absolute;
  z-index: 3;

  /* Blurr Effect */
  background:black;
  background:rgba(0,0,0,0.8);

  }

  .edit-menu {
    height: 400px;
    width: 300px;
    background-color: gray;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: end;
  }

  .buttons-container {
    display: flex;
    flex-direction: row;
  }
</style>