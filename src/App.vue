<template>
  <div id="app" class="container">
    <div class="col-md-6 col-md-offset-3">
      <img src="./assets/logo.png">
      <h2>Vue 2 Autocomplete</h2>
      <autocomplete :suggestions="suggestions" v-model="selection"></autocomplete>
    </div>
  </div>
</template>

<script>
require('../node_modules/bootstrap/dist/css/bootstrap.css')
import Autocomplete from './components/Autocomplete'

export default {
  name: 'app',
  components: {
    Autocomplete
  },
  data () {
    return {
      selection: '',
      suggestions: [
        { city: 'Bangalore', state: 'Karnataka' },
        { city: 'Chennai', state: 'Tamil Nadu' },
        { city: 'Delhi', state: 'Delhi' },
        { city: 'Kolkata', state: 'West Bengal' },
        { city: 'Mumbai', state: 'Maharashtra' }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
