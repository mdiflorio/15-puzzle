<template>
  <button class="tile" :hidden="tileHidden" :disabled="tileHidden">
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
}
</script>

<style scoped lang="scss">
.tile {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: gray;

  height: 10rem;
  margin: 0.1em;
  font-size: 2rem;
}
</style>
