<template>
  <h1>Casino Royale</h1>
  <div class="row">
    <span>Credit:</span>
    <Transition name="credit" mode="out-in">
      <span class="credit" :key="credit">{{ credit }}</span>
    </Transition>
    <div class="msg">
      <div class="error" v-if="showError">* To play, you need credit.</div>
      <div class="info" v-if="showMsg">
        Congratulations on your successful cash-out!
      </div>
    </div>
  </div>

  <div class="row">
    <Spinner :size="100" v-if="isSpinning[1]" />
    <Block :symbol="symbolMap.get(1)" v-else />

    <Spinner :size="100" v-if="isSpinning[2]" />
    <Block :symbol="symbolMap.get(2)" v-else />

    <Spinner :size="100" v-if="isSpinning[3]" />
    <Block :symbol="symbolMap.get(3)" v-else />

    <Button color="green" size="small" text="PUSH" @i-click="roll()" />
  </div>
  <div class="row" style="flex-direction: column">
    <CashOut @i-click="cashOut()" />
  </div>
</template>

<script setup>
import { ref, provide, reactive, computed, watch } from "vue";
import Block from "./components/Block.vue";
import Button from "./components/Button.vue";
import CashOut from "./components/TheCashOut.vue";
import Spinner from "./components/Spinner.vue";

// Reactive variables
const credit = ref(10);
const reward = ref(0);
const showError = ref(false);
const showMsg = ref(false);
const isSpinning = reactive({ 1: false, 2: false, 3: false });

// Computed property to check if any spinner is active
const isAnySpinning = computed(() => {
  return Object.values(isSpinning).some((s) => s);
});

// Watcher for isAnySpinning
watch(isAnySpinning, (v) => {
  if (!v) {
    credit.value += reward.value;
  }
});

// Items and SymbolMap
const items = [
  {
    name: "cherry",
    reward: 10,
  },
  {
    name: "lemon",
    reward: 20,
  },
  {
    name: "orange",
    reward: 30,
  },
  {
    name: "watermelon",
    reward: 40,
  },
];
const symbolMap = new Map();

// Function to get a random number between min (inclusive) and max (exclusive)
const getRandomNumber = (min, max) => {
  return Math.random() * (max - min) + min;
};

// Function to get a random item from items
const getRandomItem = () => {
  const i = Math.floor(getRandomNumber(0, items.length));
  return items[i]["name"];
};

// Function to show symbol for a given duration
const showSymbol = (i, t) => {
  setTimeout(() => {
    isSpinning[i] = false;
  }, t * 1000);
};

// Initialize symbolMap
symbolMap.set(1, getRandomItem());
symbolMap.set(2, getRandomItem());
symbolMap.set(3, getRandomItem());

// Function to cash out
const cashOut = () => {
  if (credit.value > 0) {
    credit.value = 0;
    showError.value = false;
    showMsg.value = true;
  }
};

// Function to roll
const roll = () => {
  reward.value = 0;
  if (isAnySpinning.value) return;
  if (credit.value === 0) {
    showError.value = true;
    showMsg.value = false;
    return;
  }

  isSpinning[1] = true;
  isSpinning[2] = true;
  isSpinning[3] = true;

  let item1 = getRandomItem();
  let item2 = getRandomItem();
  let item3 = getRandomItem();

  if (item1 === item2 && item1 === item3) {
    let mustReroll = false;
    if (credit.value >= 40 && credit.value <= 60) {
      const chance = Math.random();
      if (chance < 0.3) {
        mustReroll = true;
      }
    } else if (credit.value > 60) {
      const chance = Math.random();
      if (chance < 0.6) {
        mustReroll = true;
      }
    }

    if (mustReroll) {
      item1 = getRandomItem();
      item2 = getRandomItem();
      item3 = getRandomItem();
    }

    if (item1 === item2 && item1 === item3) {
      reward.value = items.find((i) => i["name"] === item1)["reward"];
    } else {
      reward.value = -1;
    }
  } else {
    reward.value = -1;
  }

  symbolMap.set(1, item1);
  symbolMap.set(2, item2);
  symbolMap.set(3, item3);

  showSymbol(1, 1);
  showSymbol(2, 2);
  showSymbol(3, 3);
};

provide("getRandomNumber", getRandomNumber);
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
}
.row {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 7px;
  margin-bottom: 40px;
  position: relative;
}

.info {
  color: green;
}

.error {
  color: red;
}
.msg {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  top: 20px;
}
.credit {
  width: 35px;
  font-weight: bold;
  display: inline-block;
  &-enter-from,
  &-leave-to {
    opacity: 0;
  }
  &-enter-active {
    transition: opacity 0.5s ease-in-out;
  }
  &-enter-leave {
    transition: opacity 0.4s ease-in-out;
  }
}
</style>
<style>
body {
  padding-top: 60px;
  min-height: 700px;
  min-width: 850px;
}
p {
  margin: 0;
}
</style>
