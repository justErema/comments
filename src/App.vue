<template>
  <div id="app">
    <div class="container">
      <comments></comments>
    </div>
  </div>
</template>

<script>
import Comments from './views/product/Comments.vue';

export default {
  name: 'app',

  components: { Comments },

  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.container {
  max-width: 800px;
  margin: 0 auto;
}

.btn {
  cursor: pointer;
  outline: none !important;
  border: none;
  padding: 10px 20px;
  box-shadow: none;
  text-transform: uppercase;
  &-success {
    background: #42b983;
    color: white;
  }
  &-primary {
    background: blue;
    color: white;
  }
  &-danger {
    background: red;
    color: white;
  }
}
</style>
