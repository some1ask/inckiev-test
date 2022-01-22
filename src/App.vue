<template>
  <div id="app">
    <Movie/>
  </div>
</template>

<script>

import Movie from './components/Movie.vue'
export default {
  name: 'App',
  components: {
    Movie
  }
}
</script>

<style>
#app {
  font-family: Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue",sans-serif;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
  
</style>
