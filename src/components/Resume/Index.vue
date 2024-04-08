<template>
  <main>
    <p>{{ labelContent }}</p>
    <h1 :class="showAmount < 0 ? 'danger' : 'success'">{{ visualAmount }}</h1>
  </main>
</template>

<script>
export default {
  name: "ResumeComponent",
  props: {
    label: String,
    amount: {
      type: Number,
      default: null,
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
    visualAmount() {
      return new Intl.NumberFormat("es-ES", {
        style: "currency",
        currency: "EUR"
      }).format(this.showAmount);
    },
    labelContent() {
      return this.amount ? this.date : this.label
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
</style>
