//// filepath: /home/mihadev/code/StarWarsApp/components/AppMenu.vue
<script setup lang="ts">
  import AppButton from './AppButton.vue';
  import { defineEmits, defineProps, reactive, watch, onUnmounted } from "vue";
  import type { PropType } from "vue";

  interface Character {
    name: string;
    height: string;
    mass: string;
    hair_color: string;
    skin_color: string;
    eye_color: string;
    birth_year: string;
    gender: string;
    image: string;
  }

  const props = defineProps({
    selectedCharacter: {
      type: Object as PropType<Character | null>
    }
  });

  const emit = defineEmits(["toggle-menu-off"]);

  // Create a reactive local copy for editing.
  const localCharacter = reactive({ ...props.selectedCharacter }) as Character;

  // Watch changes on the local copy.
  watch(
  localCharacter,
  () => {
    console.log("Local character changed:");
  },
  { deep: true }
);
  onUnmounted(() => console.log("off"));  
</script>

<template>
  <div class="overlay-container">
    <div class="edit-menu-container">
      <h1>Edit Character</h1>
      <div class="form-container">
        <div class="form-group">
          <p>Name:</p>
          <!-- Now use v-model to bind the local reactive copy -->
          <input type="text" v-model="localCharacter.name" />
        </div>
        <div class="form-group">
          <p>Height:</p>
          <input type="text" v-model="localCharacter.height" />
        </div>
        <div class="form-group">
          <p>Mass:</p>
          <input type="text" v-model="localCharacter.mass" />
        </div>
        <div class="form-group">
          <p>Hair color:</p>
          <input type="text" v-model="localCharacter.hair_color" />
        </div>
        <div class="form-group">
          <p>Skin color:</p>
          <input type="text" v-model="localCharacter.skin_color" />
        </div>
        <div class="form-group">
          <p>Eye color:</p>
          <input type="text" v-model="localCharacter.eye_color" />
        </div>
        <div class="form-group">
          <p>Birth year:</p>
          <input type="text" v-model="localCharacter.birth_year" />
        </div>
        <div class="form-group">
          <p>Gender:</p>
          <input type="text" v-model="localCharacter.gender" />
        </div>
      </div>
      <div class="buttons-container">
        <AppButton @click="$emit('toggle-menu-off')" button-text="Apply" style="margin: 20px;"/>
        <AppButton @click="$emit('toggle-menu-off')" button-text="Cancel" style="margin: 20px"/>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .overlay-container {
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

  .edit-menu-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 20px;
    background-color: #1e2023;
    border-radius: 10px;
    border: 2px solid white;
  }

  h1 {
    color: white;
    font-family: Roboto;
    font-size: 24px;
    margin-bottom: 15px;
  }

  .form-container {
    display: flex;
    flex-direction: column;
    width: 100%;
  }

  .form-group {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    width: 100%;
    margin: 2px;
  }

  .form-group p {
    width: 30%;
    margin-left: 8px;
    font-family: Roboto;
    color: white;
    font-weight: bold;
  }

  .form-group input {
    width: 70%;
    padding: 5px;
    border-radius: 5px;
    margin-right: 8px;
    margin-left: 5px;
  }

  .buttons-container {
    display: flex;
    flex-direction: row;
  }
</style>