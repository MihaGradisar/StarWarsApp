<script setup lang="ts">
  import { ref, onMounted } from "vue";
  import axios from "axios";
  import AppHeader from "./components/AppHeader.vue";
  import AppCard from "./components/AppCard.vue";
  import AppMenu from "./components/AppMenu.vue";

  import yodaImage from "./assets/images/yoda.jpg";
  import darthVader from "./assets/images/darthVader.jpg";
  import obiOneKenobi from "./assets/images/obiOneKenobi.jpg";

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
    if (character) {
      selectedCharacter.value = character;
    }
  };

  onMounted(async () => {
    const stored = localStorage.getItem("characters");
    if (stored) {
      // Load from local storage if present.
      characters.value = JSON.parse(stored);
      console.log("Loaded characters from local storage");
    } else {
      const endpoints = [
        "https://swapi.dev/api/people/20",
        "https://swapi.dev/api/people/4",
        "https://swapi.dev/api/people/10"
      ];

      const images = [
        yodaImage,
        darthVader, 
        obiOneKenobi
      ];

      try {
        const responses = await Promise.all(endpoints.map(url => axios.get(url)));
        const fetchedCharacters: Character[] = responses.map((res, index) => {
          return {
            name: res.data.name,
            height: res.data.height,
            mass: res.data.mass,
            hair_color: res.data.hair_color,
            skin_color: res.data.skin_color,
            eye_color: res.data.eye_color,
            birth_year: res.data.birth_year,
            gender: res.data.gender,
            image: images[index]
          };
        });

        // Update the array and store in local storage.
        characters.value = fetchedCharacters;
        localStorage.setItem("characters", JSON.stringify(fetchedCharacters));
      } catch (error) {
        console.log(error);
      }
    }
  });
</script>

<template>
  <AppMenu 
    v-if="isMenuVisible"
    :selected-character="selectedCharacter"
    @toggle-menu-off="toggleMenu"
  />
  <AppHeader />
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