<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <!-- <HelloWorld/> -->
    <todoList/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import todoList from './components/todoList'

export default {
  name: 'App',
  components: {
    HelloWorld,
    todoList,
  }
}
</script>

<style>

* {
  box-sizing: border-box;

}

.container {
  margin: 0 auto;
  width: 600px;

}

.logo {
  display: block;
  margin: 20px auto;
  height: 75px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
