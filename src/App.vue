<template>
  <div id="app" class="container">
    <task-list/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import taskList from "./components/taskList";

export default {
  name: "app",
  components: {
    HelloWorld,
    taskList
  }
};
</script>

<style>
  * {
    box-sizing: border-box;
  }

  .container {
    max-width: 600px;
    margin: 0 auto;
  }

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 20px;
}

  .logo {
    height: 75px;
  }
</style>
