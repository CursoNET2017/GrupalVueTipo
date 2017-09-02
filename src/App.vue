<template>
  <div id="app">
    <tipo></tipo>
  </div>
</template>

<script>
import tipo from './components/Tipo/Tipo.vue'

export default {
  name: 'app',
  data() {
    return {

    }
  },
  components: {
    tipo
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;  
  color: #2c3e50;
  margin-top: 60px;
}
</style>
