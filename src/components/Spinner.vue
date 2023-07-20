<template>
  <Base :size="size">
    <defs>
      <linearGradient id="myGradient" gradientTransform="rotate(90)">
        <stop offset="5%" stop-color="#eee">
          <animate
            attributeName="stop-color"
            values="#EEEEEE; #CCCCCC; #EEEEEE"
            dur="1s"
            repeatCount="indefinite"
          ></animate>
        </stop>
        <stop offset="95%" stop-color="#aaa">
          <animate
            attributeName="stop-color"
            values="#EEEEEE; #DDDDDD; #EEEEEE"
            dur="2s"
            repeatCount="indefinite"
          ></animate>
        </stop>
      </linearGradient>
    </defs>

    <rect fill="url(#myGradient)" width="100%" height="100%" rx="20" />
    <text
      v-if="false"
      x="50%"
      y="50%"
      font-size="50"
      fill="white"
      text-anchor="middle"
      alignment-baseline="middle"
    >
      X
    </text>
    <g class="spinner">
      <path
        d="M 509.89712,493.90469 342.4913,257.78506 509.03914,18.046438 C 511.46165,14.47625 511.76446,9.928 509.64476,6.1621875 a 11.895553,11.527213 0 0 0 -10.49754,-6.11325 h -140.5563 c -3.93659,0 -7.62082,1.8584375 -9.84146,5.0373125 L 255.98736,135.86169 163.22527,5.037375 A 11.976304,11.605464 0 0 0 153.3838,0 H 12.877989 C 8.4871787,0 4.3991825,2.3475 2.3804232,6.1133125 0.26072334,9.8790625 0.56353672,14.47625 2.9860357,17.9975 L 169.48341,257.78506 2.0776085,493.90469 c -2.47297641,3.52125 -2.77579103,8.11844 -0.7065988,11.93312 C 3.4402538,509.60356 7.5282431,512 11.919054,512 H 159.59147 c 3.98705,0 7.67129,-1.90738 9.89192,-5.08625 L 255.98736,382.3005 342.54177,506.91375 C 344.76241,510.09262 348.44666,512 352.4337,512 h 147.62196 c 4.44127,0 8.4788,-2.39644 10.59849,-6.16219 2.01877,-3.81468 1.76642,-8.41187 -0.75698,-11.93312 z"
      />
    </g>
  </Base>
</template>
<script setup>
import Base from "./BaseIcon.vue";
defineProps({
  size: {
    type: Number,
  },
});
</script>
<style scoped>
@keyframes spin {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(100%);
  }
}

.spinner {
  animation: spin 450ms infinite linear;
  & > path {
    transform: translateX(25%) scale(0.5);
    fill: #6e7375;
    stroke-width: 5;
  }
}
</style>
