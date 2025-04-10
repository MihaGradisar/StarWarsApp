<script setup lang="ts">
  import AppHeader from "./components/AppHeader.vue";
  import AppCard from "./components/AppCard.vue";
  import AppMenu from "./components/AppMenu.vue";

  import yodaImage from "./assets/images/yoda.jpg";
  import darthVader from "./assets/images/darthVader.jpg";
  import obiOneKenobi from "./assets/images/obiOneKenobi.jpg";

  import axios from 'axios';
  import { ref, onMounted } from "vue";

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

  const isMenuVisible = ref(false);
  const selectedCharacter = ref<Character | null>(null);
  const characters = ref<Character[]>([]);

  const toggleMenu = (character: Character | null = null) => {
    isMenuVisible.value = !isMenuVisible.value;
    if (character != null) {
      selectedCharacter.value = character;
    }
  };

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
          const character: Character = {
            name: response.data.name,
            height: response.data.height,
            mass: response.data.mass,
            hair_color: response.data.hair_color,
            skin_color: response.data.skin_color,
            eye_color: response.data.eye_color,
            birth_year: response.data.birth_year,
            gender: response.data.gender,
            image: characterImages[index]
          };

          // Saves the character data to local storage
          localStorage.setItem('character-' + index, JSON.stringify(character)); // JSON.stringefy to store object in a local storage

          // pushes the object into your characters array
          characters.value.push(character);
        })
        .catch((error) => {
          console.log(error);
        });
    });
  });
</script>

<template>
  <AppMenu 
    v-if="isMenuVisible"
    :selected-character="selectedCharacter"
    @toggle-menu-off="toggleMenu"/>
  <AppHeader/>
  <div class="container">
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