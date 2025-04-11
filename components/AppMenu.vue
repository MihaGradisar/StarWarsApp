<script setup lang="ts">
import AppButton from './AppButton.vue'
import { defineEmits, defineProps, reactive } from "vue"
import type { PropType } from "vue"

const emit = defineEmits(["toggle-menu-off", "update-character"])

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
})

const localCharacter = reactive({ ...props.selectedCharacter }) as Character // Creates a reactive object to store the changes

const applyChanges = () => {
  emit("update-character", { ...localCharacter }) // Emits the current state of the character data
  emit("toggle-menu-off")
}
</script>

<template>
  <div class="overlay-container">
    <div class="edit-menu-container">
      <h1>Edit Character</h1>
      <div class="form-container">
        <div class="form-group">
          <p>Name:</p>
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
        <AppButton @click="applyChanges" button-text="Apply" style="margin: 20px;"/>
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
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
  background: rgba(0, 0, 0, 0.8);
}

.edit-menu-container {
  display: flex;
  flex-direction: column;
  align-items: center;
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
  margin-left: 5px;
  margin-right: 8px;
}

.buttons-container {
  display: flex;
  flex-direction: row;
}

@media (min-height: 320px) {
  .edit-menu-container {
    width: 280px;
  }

  .form-group p {
  font-size: 13px;
}
}
</style>