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
    *, ::after, ::before {
        margin: 0;
        padding: 0;
        background-color: mediumspringgreen;

    }
</style>
