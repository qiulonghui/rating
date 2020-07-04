<template>
  <div id="app">
    <Examples />
  </div>
</template>

<script>
import Examples from '../examples/index'
export default {
  name: 'App',
  components: {
    Examples,
  },
  data() {
    return {}
  },
  computed: {},
  methods: {},
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
