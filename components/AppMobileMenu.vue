<template>
  <div class="dropdown">
      <div class="dropdown-links">
        <a href="">Upcoming</a>
        <a href="">Legacy</a>
        <a href="">Merch</a>
        <a href="">About</a>
      </div>
    </div>
</template>

<style scoped>
  .dropdown {
    background-color: black;
    position: absolute;
    position: fixed;
    margin-right: auto;
    margin-top: 80px;
    z-index: 100;
    height: 100%;
    width: 40%;
  }

  .dropdown-links {
    height: 100%;
    width: 100%;
    padding: 5px;
    display: flex;
    align-items: top;
    justify-content: top;
    flex-direction: column;
    color: white;
  }

  a {
    all: unset;
    margin: 10px;
    font-family: Roboto;
    font-weight: 80;
    cursor: pointer;
    color: white;
  }
</style>