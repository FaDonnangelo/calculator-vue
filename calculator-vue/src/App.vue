<template>
  <HeaderDesign/>
  <CalculatorInstance/>
</template> 

<script>
import CalculatorInstance from './components/CalculatorInstance.vue'
import HeaderDesign from './components/HeaderDesign.vue'

export default {
  name: 'App',
  components: {
    CalculatorInstance,
    HeaderDesign
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

body{
  padding: 0;
  margin: 0;
  background-image:url("./assets/background.jpeg")
}


</style>
