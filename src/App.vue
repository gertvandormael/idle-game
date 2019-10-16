<template>
  <div id="app">
    <Game></Game>
  </div>
</template>

<script>
  import Game from './components/Game.vue'

  export default {
    name: 'app',
    components: {
      Game
    }
  }
</script>

<style>
/* General layout*/
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    margin-left: 15px;
    font-family: 'Ubuntu', sans-serif;
    background: #56965d;
    color: #cbdbfc;
    font-size: 16px;
  }

  h1 {
    font-family: 'Press Start 2P', cursive;
    font-size: 26px;
  }

  h2 {
    font-family: 'Press Start 2P', cursive;
    margin-top: 10px;
  }

  h3 {
    font-family: 'Press Start 2P', cursive;
    color: #ff6fd2;
  }

  #app {
    display: flex;
    justify-content: center;
  }
</style>