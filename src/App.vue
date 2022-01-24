<template>
  <div id="app">
    <Slider :slides="sliderItems"/>
    <Form/>
    <Movie/>
  </div>
</template>

<script>

import Slider from './components/Slider.vue'
import Form from './components/Form.vue'
import Movie from './components/Movie.vue'
export default {
  name: 'App',
  components: {
    Slider,
    Form,
    Movie
  },
  data(){
    return{
      sliderItems:[
        {id:0,color:'#027D84'},
        {id:1,color:'#4A989A'},
        {id:2,color:'#AFB3B4'}
      ]
    }
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
