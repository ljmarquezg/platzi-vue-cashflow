<template>
  <div class="graphic">
    <svg
      :viewBox="viewBox"
      @touchstart="tap"
      @touchmove="tap"
      @touchend="untap"
    >
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="zero"
        :y1="zero"
        x2="300"
        :y2="zero"
      />

      <polyline
        fill="none"
        stroke="#0689B0"
        stroke-width="2px"
        :points="points"
      />

      <line
        v-show="showPointer"
        stroke="#04b500"
        stroke-width="2px"
        :x1="pointer"
        y1="0"
        :x2="pointer"
        y2="200"
      />
    </svg>
    <p>Últimos 30 días</p>
  </div>
</template>

<script setup>
import { computed, defineProps, ref, toRefs } from "vue";

const props = defineProps({
  amounts: {
    type: Array,
    default: () => []
  }
});

const { amounts } = toRefs(props);

const width = 300;
const height = 200;
const viewBox = ref(`0 0 ${width} ${height}`);
const min = Math.min(...amounts.value);
const max = Math.max(...amounts.value);

const zero = computed(() => {
  return amountToPixels(0);
});

const amountToPixels = (amountValue) => {
  const amountAbs = amountValue + Math.abs(min);
  const amountRange = Math.abs(max) + Math.abs(min);

  return height - (((amountAbs * 100) / amountRange) * 2);
};

const points = computed(() => {
  const total = amounts.value.length;

  return amounts.value.reduce((points, amount, index) => {
    const x = (width / total) * (index + 1);
    const y = amountToPixels(amount);
    return `${points} ${x},${y}`;
  }, `0,${zero.value}`);
});

const showPointer = ref(false);
const pointer = ref(null);
// const emit = defineEmits(["select"]);
const tap = ({ target, touches }) => {
  showPointer.value = true;
  //const x = touches[0].clientX;
  const elementWidth = target.getBoundingClientRect().width;
  const elementX = target.getBoundingClientRect().x;
  const touchX = touches[0].clientX;

  pointer.value = (( touchX - elementX) * width) / elementWidth;
  // emit("select", pointer.value);
};

const untap = () => {
  showPointer.value = false;
};
</script>

<style
  lang="scss"
  scoped
>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
