<script setup lang="ts">
  // Component imports
  import AppHeader from "./components/AppHeader.vue";
  import AppCard from "./components/AppCard.vue";
  import AppMenu from "./components/AppMenu.vue";

  // Image imports
  import yodaImage from "./assets/images/yoda.jpg";
  import darthVader from "./assets/images/darthVader.jpg";
  import obiOneKenobi from "./assets/images/obiOneKenobi.jpg";

  import axios from 'axios';

  import { ref } from "vue";

  const isMenuVisible = ref(false);
  const selectedCharacter = ref<Character | null>(null); //
  const characters = ref<Character[]>([]);


  const toggleMenu = (character = null) => {
    isMenuVisible.value = !isMenuVisible.value;
    if (character != null) {
      selectedCharacter.value = character;
      console.log(selectedCharacter);
    }
  };

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

  onMounted(() => {
    console.log("Mounted");

    const characterEndpoints = [
      "https://swapi.dev/api/people/20",
      "https://swapi.dev/api/people/4",
      "https://swapi.dev/api/people/10"
    ];

    const characterImages = [
      yodaImage,
      darthVader,
      obiOneKenobi
    ];

    characterEndpoints.forEach((url, index) => {
      axios.get(url)
        .then((response) => {
          characters.value.push({
            name: response.data.name,
            height: response.data.height,
            mass: response.data.mass,
            hair_color: response.data.hair_color,
            skin_color: response.data.skin_color,
            eye_color: response.data.eye_color,
            birth_year: response.data.birth_year,
            gender: response.data.gender,
            image: characterImages[index]
          });
        })
        .catch((error) => {
          console.log(error);
        });
    });
  });

</script>

<template>
  <!-- Listents for emits. When the button is pressed the "toggle Menu" function is triggered. -->
  <AppMenu 
    v-show="isMenuVisible"
    :selected-character="selectedCharacter"
    @toggle-menu-off="toggleMenu"/>
  <AppHeader/>
  <div class="container">
    <!-- Render a card for each character -->
    <AppCard
      v-for="(character, index) in characters"
      :key="index"
      :character="character"
      @toggle-menu-on="toggleMenu"
    />
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