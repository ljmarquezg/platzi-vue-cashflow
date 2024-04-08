<template>
  <header>
    <img
      @click="reload"
      src="@/assets/logo.svg"
      alt="logo"
      class="brand-logo"
    />

    <h1><span>Cash</span>Flow</h1>

    <span></span>
  </header>
</template>
<script>
export default {
  name: "HeaderComponent",
  methods: {
    reload() {
      window.location.reload();
    }
  }
};
</script>

<style
  lang="scss"
  scoped
>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.brand-logo {
  width: 48px;
  cursor: pointer;
}

h1 {
  font-weight: 700;
  color: var(--brand-green);
  margin: 0;
  font-size: 1.4rem;

  span {
    color: var(--brand-blue);
  }
}
</style>
