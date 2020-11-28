<template>
  <div class="board" :style="style">
    <Tile v-for="tile in tiles" :key="tile" :text="tile" :tile-hidden="false" />
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
