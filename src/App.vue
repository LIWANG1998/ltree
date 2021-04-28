<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Ltree />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Ltree from "./components/ltree.vue";

@Component({
  components: {
    Ltree,
  },
})
export default class App extends Vue {}
</script>

<style lang="less">
body {
  background-color: rgb(0, 0, 0);
  color: white;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
