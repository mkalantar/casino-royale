<template>
  <div class="block">
    <component :is="cmp" :size="size" />
  </div>
</template>
<script setup>
import { computed } from "vue";
import Cherry from "./Cherry.vue";
import Lemon from "./Lemon.vue";
import Watermelon from "./Watermelon.vue";
import Orange from "./OrangeIcon.vue";
import Spinner from "./Spinner.vue";
const props = defineProps({
  symbol: String,
  size: {
    type: Number,
    default: 50,
  },
});

const cmp = computed(() => {
  switch (props.symbol.toLowerCase()) {
    case "cherry":
      return Cherry;
    case "watermelon":
      return Watermelon;
    case "orange":
      return Orange;
    case "lemon":
      return Lemon;
    case "spinner":
      return Spinner;
  }
});
</script>
<style lang="scss" scoped>
.block {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f0f0f0;
  border-radius: 5px;
}
</style>
