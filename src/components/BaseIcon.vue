<template>
  <svg
    :height="sizePx"
    :width="sizePx"
    version="1.1"
    id="Layer_1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    :viewBox="viewBox"
    xml:space="preserve"
  >
    <slot />
  </svg>
</template>
<script setup>
import { computed } from "vue";
const props = defineProps({
  /**
   * The size of the icon.
   * @type {number}
   * @default 20
   */
  size: {
    type: Number,
    default: 20,
  },
  /**
   * The viewbox of the svg.
   * @type {string}
   * @default "0 0 512 512"
   */
  viewBox: {
    type: String,
    default: "0 0 512 512",
  },
});
const sizePx = computed(() => {
  return props.size + "px";
});
</script>
