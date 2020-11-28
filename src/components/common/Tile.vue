<template>
  <button
    class="tile"
    :style="style"
    :class="{ 'tile-hidden': tileHidden }"
    :disabled="tileHidden"
    :index="index"
    @click="handleClick"
  >
    {{ text }}
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Tile extends Vue {
  @Prop({ type: [String, Number] })
  private text!: string | number;

  @Prop({ type: Boolean })
  private tileHidden!: boolean;

  @Prop({ type: String })
  gridPos!: string;

  @Prop({ type: Number, default: 0 })
  index!: number;

  get style() {
    return {
      "--grid-pos": this.gridPos
    };
  }

  handleClick() {
    this.$emit("click", this.index);
  }
}
</script>

<style scoped lang="scss">
.tile {
  grid-column: var(--grid-pos);

  display: flex;
  justify-content: center;
  align-items: center;
  background-color: gray;

  height: 10rem;
  margin: 0.1em;
  font-size: 2rem;

  &-hidden {
    visibility: hidden;
  }
}
</style>
