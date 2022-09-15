<template>

  <earth />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import earth from "@/components/earth";
export default {
  name: 'App',
  components: {
    HelloWorld,
    earth
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
