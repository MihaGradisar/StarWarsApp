<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'
import AppHeader from './components/AppHeader.vue'
import AppCard from './components/AppCard.vue'
import AppMenu from './components/AppMenu.vue'

import yodaImage from './assets/images/yoda.jpg'
import darthVader from './assets/images/darthVader.jpg'
import obiOneKenobi from './assets/images/obiOneKenobi.jpg'

// Set the Character interface.
interface Character {
  id: number
  name: string
  height: string
  mass: string
  hair_color: string
  skin_color: string
  eye_color: string
  birth_year: string
  gender: string
  image: string
}

// State variables.
const isMenuVisible = ref(false)
const selectedCharacter = ref<Character | null>(null)
const characters = ref<Character[]>([])

// loads data from local storage or fetches the data from API.
onMounted(async () => {
  const storedCharacters = localStorage.getItem('characters')
  if (storedCharacters) { // Checks if storedCharacters contains a value
    characters.value = JSON.parse(storedCharacters) // Loads the local data in the characters variable
  } else {
    const endpoints = [
      'https://swapi.dev/api/people/20',
      'https://swapi.dev/api/people/4',
      'https://swapi.dev/api/people/10'
    ]

    const images = [
      yodaImage,
      darthVader,
      obiOneKenobi
    ]

    // Fetches the data from endpoints
    const responses = await Promise.all(
      endpoints.map(url => axios.get(url))
    )
    
    // Builds the array of characters
    let fetchedCharacters: Character[] = [] 
    responses.forEach((response, index) => {
      fetchedCharacters.push({
        id: index + 1,
        name: response.data.name,
        height: response.data.height,
        mass: response.data.mass,
        hair_color: response.data.hair_color,
        skin_color: response.data.skin_color,
        eye_color: response.data.eye_color,
        birth_year: response.data.birth_year,
        gender: response.data.gender,
        image: images[index]
      })
    })
    characters.value = fetchedCharacters // Pushes the data in characters variable
    localStorage.setItem('characters', JSON.stringify(fetchedCharacters)) // Stores the data in local storage
  }
})

// Toggle the menu. If a character is supplied, set it as selected.
const toggleMenu = (character: Character | null = null) => {
  isMenuVisible.value = !isMenuVisible.value
  if (character) {
    selectedCharacter.value = character
  }
}

// Update a character in the list.
const updateCharacter = (updated: Character) => { // Takes in the data that was passed by AppMenu.vue 
  characters.value.forEach((character, index) => { // Goes threw the array
    if (character.id === updated.id) { // Finds the maching id
      characters.value[index] = updated // Updates the correct chracter data
    }
  })
  localStorage.setItem('characters', JSON.stringify(characters.value)) // Updates the local storage with updated data
}
</script>

<template>
  <AppMenu 
    v-if="isMenuVisible"
    :selected-character="selectedCharacter"
    @toggle-menu-off="toggleMenu"
    @update-character="updateCharacter"
  />
  <AppHeader />
  <div class="app-container">
    <div class="card-container">
    <AppCard 
      v-for="character in characters"
      :key="character.id"
      :character="character"
      @toggle-menu-on="toggleMenu"
    />
  </div>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  width: 100vw;
  background: radial-gradient(circle 370px at center, yellow -300%, #000 100%);
  background-size: cover;
  background-repeat: no-repeat;
  position: relative;
}

.card-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  width: 100%;
  min-height: 100%;
  margin-top: 100px;
}

</style>