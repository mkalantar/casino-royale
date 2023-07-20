<template>
  <div class="container" :style="style">
    <Button
      size="large"
      text="CASH OUT"
      @mouseover="mouseOver()"
      @i-click="$emit('i-click')"
      :enable="enable"
    />
  </div>
</template>

<script setup>
import { ref, inject } from "vue";
import Button from "./Button.vue";

const getRandomNumber = inject("getRandomNumber");
const emit = defineEmits(["i-click"]);

const enable = ref(true);
const style = ref("");

const makeButtonUnclickable = () => {
  enable.value = false;
};

const moveButton = () => {
  const dx = getRandomNumber(-300, 300);
  const dy = getRandomNumber(-300, 300);

  style.value = `transform: translate(${dx}px, ${dy}px);`;
};

const mouseOver = () => {
  const chance = Math.random();

  // 50% chance of moving the button in a random direction by 300px
  if (chance < 0.5) {
    moveButton();
  }
  // 40% chance of making the button unclickable
  else if (chance < 0.9) {
    makeButtonUnclickable();
  }
};
</script>

<style scoped>
.container {
  display: flex;
}
</style>
