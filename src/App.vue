<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <HelloWorld msg="Vue3 App by Bigliuliu & Henryhe" />
  <div>
    <p>-------------mySql learning------------------</p>
    <my-sql-vue />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import mySqlVue from "./components/mySql.vue";
export default {
  name: "App",
  components: {
    HelloWorld,
    mySqlVue,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  padding-left: 20%;
  h3,
  h4 {
    color: red;
  };
  p{
    font-weight: bold;
  }
}
</style>
