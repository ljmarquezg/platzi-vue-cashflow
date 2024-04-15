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
        x1="0"
        :y1="zero || 0"
        :x2="width"
        :y2="zero || 0"
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
        :y2="height || 0"
      />
    </svg>
    <p>Últimos 30 días</p>
  </div>
</template>

<script setup>
import { computed, defineEmits, defineProps, ref, toRefs, watch } from "vue";

const props = defineProps({
  amounts: {
    type: Array,
    default: () => [0]
  }
});

const { amounts } = toRefs(props);

const width = 300;
const height = 200;
const viewBox = ref(`0 0 ${width} ${height}`);

const zero = computed(() => {
  return amountToPixels(0);
});

const amountToPixels = (amountValue) => {
  const min = Math.min(...amounts.value);
  const max = Math.max(...amounts.value);
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
  }, `0,${amounts.value.length ? amountToPixels(amounts.value[0]) : zero.value}`);
});

const showPointer = ref(false);
const pointer = ref(null);
const emit = defineEmits(["select"]);

watch(pointer, (value) => {
  const amountLength = amounts.value.length;
  const index = Math.ceil(value / (width / amountLength));

  if (index > 0 || index < amountLength) {
    emit("select", amounts.value[index - 1]);
  }
});

const tap = ({ target, touches }) => {
  showPointer.value = true;
  const elementWidth = target.getBoundingClientRect().width;
  const elementX = target.getBoundingClientRect().x;
  const touchX = touches[0].clientX;

  pointer.value = ((touchX - elementX) * width) / elementWidth;
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
