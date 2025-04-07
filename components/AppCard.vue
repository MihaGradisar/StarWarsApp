<script setup lang="ts">
  import { defineEmits } from "vue";
  import AppButton from "./AppButton.vue";

  defineEmits(["toggle-menu"]);

  defineProps({
    character: Object,
  });

</script>

<template>
  <div class="card">
    <img :src="character?.image" />
    <div class="character-info-container">
      <p>Name: <span> {{ character?.name }} </span></p>
      <p>Height: <span> {{ character?.height }} </span></p>
      <p>Mass: <span> {{ character?.mass }} </span></p>
      <p>Hair color: <span> {{ character?.hair_color }} </span></p>
      <p>Skin color: <span> {{ character?.skin_color }} </span></p>
      <p>Eye color: <span> {{ character?.eye_color }} </span></p>
      <p>Birth year: <span> {{ character?.birth_year }} </span></p>
      <p>Gender: <span> {{ character?.gender }} </span></p>
    </div>
    <div class="button-container">
      <!-- Triggers an emit with the ewnet handler -->
      <AppButton buttonText="Edit" @click="$emit('toggle-menu')" />
    </div>
  </div>
</template>

<style scoped>
  .card {
    position: relative;
    height: 420px;
    width: 185px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    justify-content: end;
    margin: 10px;
    border-radius: 10px;
  }

  img {
    position: absolute;
    width: 200px;
  }

  .character-info-container {
    display: flex;
    flex-direction: column;
    justify-content: end;
    position: relative;
    z-index: 2;
    padding-left: 10px;
  }

  .character-info-container p {
    color: white;
    font-family: Roboto;
    font-size: 14px;
    padding-top: 3px;
  }

  .character-info-container p span {
    font-weight: bold;
  }

  .button-container {
    position: relative;
    z-index: 2;
    display: flex;
    justify-content: center;
    margin: 20px;
  }
</style>