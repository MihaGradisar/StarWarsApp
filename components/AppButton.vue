<script setup lang="ts">
// Button props
defineProps({
  buttonText: {
    type: String,
    default: 'button'
  }
});
</script>

<template>
  <div class="button">
    {{ buttonText }}
  </div>
</template>

<style scoped>
  .button {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #e3d61d;
    height: 30px;
    width: 100px;
    font-family: Roboto;
    font-size: 18px;
    font-weight: bold;
    z-index: 2;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.2s ease-in-out;
  }

  .button:hover {
    background-color: #817a18;
  }
</style>