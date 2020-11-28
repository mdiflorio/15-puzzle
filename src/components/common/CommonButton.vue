<template>
  <button class="common_btn" @click="$emit('click')">
    {{ text }}
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class CommonButton extends Vue {
  @Prop({ type: [String, Number] })
  private text!: string | number;
}
</script>

<style scoped lang="scss">
.common_btn {
}
</style>
