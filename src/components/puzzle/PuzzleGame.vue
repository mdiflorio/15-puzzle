<template>
  <Board :tiles="boardState" :col-size="colSize" @move-tile="moveTile" />
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
  emptyTilePos!: number;

  created() {
    this.boardLength = this.colSize * this.colSize;
    this.emptyTilePos = this.colSize * this.colSize - 1;
    this.initBoards();
  }

  initBoards() {
    for (let i = 0; i < this.boardLength; i++) {
      this.boardState.push(i);
      this.boardObjective.push(i);
    }
    this.scrambleBoard();
  }

  moveTile(tileIndex: number) {
    const canMove = this.possibleMoves().includes(tileIndex);

    if (canMove) {
      const tileNumber = this.boardState[tileIndex];

      // Swap the tile with the empty spot
      Vue.set(this.boardState, this.emptyTilePos, tileNumber);
      Vue.set(this.boardState, tileIndex, this.boardLength - 1);

      this.emptyTilePos = tileIndex;
    }
  }

  possibleMoves() {
    const emptyTilePos = this.emptyTilePos;

    // Get index of tiles around the empty tile
    const aboveEmptyTile = emptyTilePos - this.colSize;
    const belowEmptyTile = emptyTilePos + this.colSize;
    const leftEmptyTile = emptyTilePos - 1;
    const rightEmptyTile = emptyTilePos + 1;

    const moves = [
      aboveEmptyTile,
      belowEmptyTile,
      leftEmptyTile,
      rightEmptyTile
    ];

    // Remove all indexes that are out of the board
    return moves.filter(index => index >= 0 && index <= this.boardLength);
  }

  scrambleBoard() {
    this.boardState = this.boardState
      .map(a => ({ sort: Math.random(), value: a }))
      .sort((a, b) => a.sort - b.sort)
      .map(a => a.value);

    this.emptyTilePos = this.boardState.findIndex(
      tile => tile === this.boardLength - 1
    );
  }

  // checkHasWon() {
  //
  // }
}
</script>

<style scoped lang="scss"></style>
