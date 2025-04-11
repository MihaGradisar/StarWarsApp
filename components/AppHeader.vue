<template>
  <div class="header-container">
    <span class="material-icons">menu</span>
    <span><a href="">Upcoming</a></span>
    <span><a href="">Legacy</a></span>
    <img src="../assets/images/logo.png" alt="Star Wars Logo">
    <span><a href="">Merch</a></span>
    <span><a href="">About</a></span>
  </div>
</template>

<style scoped>
  .header-container {
    z-index: 99;
    height: 80px;
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
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

  .material-icons {
    color: white;
    font-size: 40px;
    margin-right: auto;
    margin-left: 20px;
  }

  @media (min-height: 620px) {
    .material-icons {
      display: none;
    }
  }

  @media (max-height: 620px) {
    .header-container {
      background-color: black;
    }

    span a {
      display: none;
    }

    img {
      position: absolute;
    }
  }
</style>