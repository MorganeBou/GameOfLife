<template>
  <div id="app">
      <div> Le Game of life </div>

    <GameOfLife/>

  </div>
</template>

<script>
import GameOfLife from './components/GameOfLife.vue'

export default {
  name: 'App',
  components: {
    GameOfLife
  }
}
</script>

<style>
    body{
      margin: 0;
    }
</style>
