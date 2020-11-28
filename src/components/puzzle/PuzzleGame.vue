<template>
  <div class="puzzle_game"></div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class PuzzleGame extends Vue {
  @Prop() private msg!: string;
}
</script>

<style scoped lang="scss">
.puzzle_game {
}
</style>
