<template>
  <div class="header-container">
    <span><a href="">Upcoming</a></span>
    <span><a href="">Legacy</a></span>
    <img src="../assets/images/logo.png" alt="Star Wars Logo">
    <span><a href="">Merch</a></span>
    <span><a href="">About</a></span>
  </div>
</template>

<style scoped>
  .header-container {
    position: absolute;
    height: 80px;
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  a {
    all: unset;
    font-family: Roboto;
    font-weight: 80;
    cursor: pointer;
    color: white;
    margin: 25px;
  }

  img {
    width: 150px;
    margin: 25px;
  }
</style>