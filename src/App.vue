<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  position: relative;
  width: 100%;
  max-width: 1366px;
  margin: 0 auto;
  padding: 0 20px;
}
img {
  height: auto;
  max-width: 100%;
}
.flex {
  display: flex;
}
.space-between {
  justify-content: space-between;
}
.flex-end {
  justify-content: flex-end;
}
</style>
