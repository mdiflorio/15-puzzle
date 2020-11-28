<template>
  <div class="banner">
    {{ text }}
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Banner extends Vue {
  @Prop({ type: [String] })
  private text!: string;
}
</script>

<style scoped lang="scss">
.banner {
}
</style>
