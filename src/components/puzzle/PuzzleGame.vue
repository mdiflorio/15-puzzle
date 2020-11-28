<template>
  <div class="puzzle_game">
    <Banner v-if="hasWon" text="Congradulations you've won!" />
    <div class="btn_container">
      <CommonButton text="Reset" @click="initBoards" />
      <CommonButton text="Scramble board" @click="scrambleBoard" />
    </div>
    <Board :tiles="boardState" :col-size="colSize" @move-tile="moveTile" />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { PuzzleTiles } from "@/app.types";
import Board from "@/components/common/Board.vue";
import Banner from "@/components/common/Banner.vue";
import CommonButton from "@/components/common/CommonButton.vue";

@Component({
  components: { Board, Banner, CommonButton }
})
export default class PuzzleGame extends Vue {
  @Prop({ default: 3, type: Number })
  private colSize!: number;

  boardLength!: number;
  boardObjective: PuzzleTiles = [];
  boardState: PuzzleTiles = [];

  hasWon = false;
  emptyTilePos!: number;

  created() {
    this.boardLength = this.colSize * this.colSize;
    this.initBoards();
  }

  // Initialise the boards to their starting state
  initBoards() {
    this.boardState = [];
    this.boardObjective = [];
    for (let i = 0; i < this.boardLength; i++) {
      this.boardState.push(i);
      this.boardObjective.push(i);
    }
    this.setEmptyTilePos();
  }

  // Move tile into the empty spot
  moveTile(tileIndex: number) {
    const canMove = this.possibleMoves().includes(tileIndex);

    if (canMove) {
      const tileNumber = this.boardState[tileIndex];

      // Swap the tile with the empty spot
      Vue.set(this.boardState, this.emptyTilePos, tileNumber);
      Vue.set(this.boardState, tileIndex, this.boardLength - 1);

      this.emptyTilePos = tileIndex;
      this.hasWon = this.checkHasWon();
    }
  }

  // Get the indexes of the tiles that can be moved into the empty spot
  possibleMoves() {
    const emptyTilePos = this.emptyTilePos;

    // Get index of the tiles around the empty tile
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

  // Scramble the board state.
  scrambleBoard() {
    // Randomise the array
    this.boardState = this.boardState
      .map(a => ({ sort: Math.random(), value: a }))
      .sort((a, b) => a.sort - b.sort)
      .map(a => a.value);

    this.setEmptyTilePos();
  }

  // Check the board state against the board objective
  checkHasWon(): boolean {
    for (let i = 0; i < this.boardLength; i++) {
      if (this.boardState[i] !== this.boardObjective[i]) {
        return false;
      }
    }
    return true;
  }

  // Find the empty tile position
  setEmptyTilePos() {
    this.emptyTilePos = this.boardState.findIndex(
      tile => tile === this.boardLength - 1
    );
  }
}
</script>

<style scoped lang="scss">
.puzzle_game {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  .btn_container {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>
