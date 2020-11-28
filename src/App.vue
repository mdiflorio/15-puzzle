<template>
  <div id="app">
    <PuzzleGame :col-size="3" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/puzzle/PuzzleGame.vue";
import PuzzleGame from "@/components/puzzle/PuzzleGame.vue";

@Component({
  components: {
    PuzzleGame
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
