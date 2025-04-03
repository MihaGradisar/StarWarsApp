<script setup lang="ts">
  import AppEditButton from "./AppEditButton.vue"
</script>

<template>
  <div class="card">
    <div class="character-info">
      <p>Name: <span> {{ "Yoda" }} </span></p>
      <p>Height: <span> {{ "66cm" }} </span></p>
      <p>Mass: <span> {{ "13kg" }} </span></p>
      <p>Hair color: <span> {{ "White" }} </span></p>
      <p>Skin color: <span> {{ "Green" }} </span></p>
      <p>Eye color: <span> {{ "Green-gold" }} </span></p>
      <p>Birth year: <span> {{ "896 BBY" }} </span></p>
      <p>Gender: <span> {{ "Male" }} </span></p>
    </div>
    <img src="../assets/images/yoda.jpg" alt="Yoda">
  </div>
</template>

<style scoped>
  .card {
    height: 450px;
    width: 210px;
    display: flex;
    justify-content: start;
    align-items: end;
  }

  .character-info {
    z-index: 999;
    padding: 15px;
  }

  .character-info p {
    color: white;
    font-family: Roboto;
    font-size: 15px;
  }

  .character-info p span {
    font-weight: bold;
  }

  img {
    height: 450px;
    width: 210px;
    border-radius: 10px;
    position: absolute;
    z-index: 1;
  }
</style>