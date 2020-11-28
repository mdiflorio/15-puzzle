<template>
  <div class="board" :style="style">
    <Tile
      v-for="(tile, index) in tiles"
      :key="tile"
      :text="tile"
      :tile-hidden="tile === tiles.length - 1"
      :index="index"
      :grid-pos="calculateTilePos(index)"
      @click="handleTileClick"
    />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { PuzzleTiles } from "@/app.types";
import Tile from "@/components/common/Tile.vue";

@Component({
  components: { Tile }
})
export default class Board extends Vue {
  @Prop({ type: Array, default: [] })
  private tiles!: PuzzleTiles;

  @Prop({ type: Number })
  private colSize!: number;

  get style() {
    return {
      // Variable used in css
      "--col-size": this.colSize
    };
  }

  calculateTilePos(tileIndex: number): string {
    const col = tileIndex / this.colSize;
    const row = tileIndex % this.colSize;
    return `${col} / ${row}`;
  }

  handleTileClick(tileIndex: number) {
    this.$emit("move-tile", tileIndex);
  }
}
</script>

<style scoped lang="scss">
.board {
  display: grid;
  grid-template-columns: repeat(var(--col-size), 1fr);
  grid-template-rows: repeat(var(--col-size), 1fr);
  width: 90%;
  max-width: 500px;
}
</style>
