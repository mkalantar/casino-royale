<template>
  <a
    href=""
    class="btn-push"
    :class="[color, size, { disable }]"
    @mouseover="$emit('mouseover')"
    @click.prevent="click()"
  >
    {{ text }}
  </a>
</template>

<script setup>
import { computed } from "vue";

const emit = defineEmits(["i-click", "mouseover"]);
const props = defineProps({
  /**
   * The color of the button.
   * @type {string}
   * @default ""
   */
  color: {
    type: String,
    default: "",
  },

  /**
   * Enable or disable the button.
   * @type {boolean}
   * @default true
   */
  enable: {
    type: Boolean,
    default: true,
  },

  /**
   * The size of the button.
   * @type {string}
   * @default "large"
   */
  size: {
    type: String,
    default: "large",
  },

  /**
   * The text to display inside the button.
   * @type {string}
   * @required
   */
  text: {
    type: String,
    required: true,
  },
});

const disable = computed(() => {
  return !props.enable;
});

const click = () => {
  if (props.enable) {
    emit("i-click");
  }
};
</script>

<style scoped>
.btn-push {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  top: 0px;
  text-decoration: none;
  font-size: 25px;
  background: #f7f7f7;
  border: 1px solid #c4c4c4;
  border-radius: 5px;
  box-shadow: 0px 5px 0px #c4c4c4;
  color: #222;
  text-shadow: 1px 1px 1px #fff;
  transition: all 250ms ease;
  box-sizing: border-box;
  user-select: none;
}

.btn-push:active {
  position: relative;
  top: 5px;
  box-shadow: none !important;
  transition: all 250ms ease;
}

.btn-push.green {
  background: #7cc576;
  color: #fff;
  border: 1px solid #46963f;
  border-radius: 5px;
  box-shadow: 0px 5px 0px #46963f;
  text-shadow: 1px 1px 1px #46963f;
}

.btn-push.small {
  width: 45px;
  height: 30px;
  font-size: 15px;
}

.btn-push.large {
  width: 120px;
  height: 50px;
  font-size: 20px;
}

.btn-push.disable {
  cursor: not-allowed;
}
</style>
