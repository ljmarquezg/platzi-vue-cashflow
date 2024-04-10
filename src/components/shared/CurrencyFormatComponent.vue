<template>
  <span :class="{
    'text-success' : !isNegative,
    'text-danger': isNegative
  }">
    {{ amountCurrency }}
  </span>
</template>
<script setup>
import { defineProps, toRefs, computed } from "vue";

const props = defineProps({
  amount: {
    type: Number,
    default: () => {
    }
  }
});

const amountCurrency = computed(() => {
  return new Intl.NumberFormat("es-ES", {
    style: "currency",
    currency: "EUR"
  }).format(amount.value);
});

const isNegative = computed(() => {
  return amount.value < 0;
});

const { amount } = toRefs(props);
</script>
