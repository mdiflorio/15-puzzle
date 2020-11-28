<template>
  <Board :tiles="boardState" :col-size="colSize" />
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { PuzzleTiles } from "@/app.types";
import Board from "@/components/common/Board.vue";

@Component({
  components: { Board }
})
export default class PuzzleGame extends Vue {
  @Prop({ default: 3, type: Number })
  private colSize!: number;

  boardLength!: number;

  boardObjective: PuzzleTiles = [];
  boardState: PuzzleTiles = [];

  created() {
    this.boardLength = this.colSize * this.colSize;
    this.initBoards();
  }

  initBoards() {
    for (let i = 0; i < this.boardLength; i++) {
      this.boardState.push(i);
      this.boardObjective.push(i);
    }
  }
}
</script>

<style scoped lang="scss"></style>
