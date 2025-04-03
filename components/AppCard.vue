<script setup lang="ts">
  import AppEditButton from "./AppEditButton.vue"
</script>

<template>
  <div class="card">
    <img src="../assets/images/yoda.jpg" alt="">
    <div class="character-info-container">
      <p>Name: <span> {{ "Yoda" }} </span></p>
      <p>Height: <span> {{ "66cm" }} </span></p>
      <p>Mass: <span> {{ "13kg" }} </span></p>
      <p>Hair color: <span> {{ "White" }} </span></p>
      <p>Skin color: <span> {{ "Green" }} </span></p>
      <p>Eye color: <span> {{ "Green-gold" }} </span></p>
      <p>Birth year: <span> {{ "896 BBY" }} </span></p>
      <p>Gender: <span> {{ "Male" }} </span></p>
    </div>
    <div class="button-container">
      <AppEditButton/>
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
    z-index: 999;
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
    z-index: 999;
    display: flex;
    justify-content: center;
    margin: 20px;
  }
</style>