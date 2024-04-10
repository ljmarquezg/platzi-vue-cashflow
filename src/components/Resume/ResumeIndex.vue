<template>
  <main>
    <p>{{ visualLabel }}</p>
    <h1>
      <CurrencyFormatComponent :amount="showAmount"/>
    </h1>
    <div class=" graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="action"></slot>
    </div>
  </main>
</template>

<script>
import CurrencyFormatComponent from "@/components/CurrencyFormatComponent.vue";

export default {
  name: "ResumeIndex",
  components: { CurrencyFormatComponent },
  props: {
    label: {
      type: String,
      default: null
    },
    totalLabel: String,
    amount: {
      type: Number,
      default: null
    },
    totalAmount: {
      type: Number,
      default: 0
    },
    date: {
      type: String,
      default: new Date().toLocaleDateString()
    }
  },
  computed: {
    showAmount() {
      return this.amount || this.totalAmount;
    },
    visualLabel() {
      return this.amount ? this.date : this.label;
    }
  }
};
</script>

<style
  lang="scss"
  scoped
>

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  margin: 16px 0;
}

h1 {
  font-size: 2.5rem;
  margin: 0;
}

p {
  margin: 0;
}
</style>
