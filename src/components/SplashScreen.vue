<template>
  <div class="splash-screen">
    <img src="@/assets/logo.svg" alt="CashFlow logo" />
    <h1 class="title"><span>Cash</span>Flow</h1>
  </div>
</template>

<script>
export default {
  name: "SplashScreen",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style
  scoped
  lang="scss"
>
.splash-screen {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100dvh;
}

.title {
  margin: 40px 0 0;
  color: var(--brand-green);

  span {
    color: var(--brand-blue);
  }
}
</style>
