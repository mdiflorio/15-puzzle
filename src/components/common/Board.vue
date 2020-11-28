<template>
  <div class="board"></div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Board extends Vue {
  @Prop() private msg!: string;
}
</script>

<style scoped lang="scss">
.board {
}
</style>
