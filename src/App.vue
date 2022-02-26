<template>
  <Vuelidate />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Vuelidate from './components/Vuelidate.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    Vuelidate
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
  margin-top: 60px;
}
</style>
