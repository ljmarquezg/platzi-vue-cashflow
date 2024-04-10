<template>
  <Suspense>
    <template #default>
      <HomeComponent />
    </template>
    <template #fallback>
      <SplashScreen />
    </template>
  </Suspense>
</template>

<script>
import { defineAsyncComponent } from "vue";
import SplashScreen from "./components/SplashScreen.vue";

export default {
  name: "App",
  components: {
    SplashScreen,
    HomeComponent: defineAsyncComponent(() => new Promise(
      (resolve) => setTimeout(() => resolve(import("./components/Home.vue")), 2000)
    ))
  }
};
</script>

<style lang="scss">
@import "https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0";
* {
  box-sizing: border-box;
}

body, html, #app {
  margin: 0;
  padding: 0;
  font-size: 16px;
  line-height: 1.5;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.material-symbols-outlined {
  font-variation-settings: "FILL" 0,
  "wght" 400,
  "GRAD" 0,
  "opsz" 24
}

:root {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
  --brand-danger: #b00e2d;
  --brand-success: #17b006;
  --border-color: #ccc;
  --muted-color: #63646f;
  --light-background-color: #e5e5e5;
  --movement-background-color: #ccc;
  --movement-item-background-color: #f2f2f2;
  --box-shadow: rgba(17, 17, 26, 0.05) 0px 4px 16px, rgba(17, 17, 26, 0.05) 0px 8px 32px;
}

.text-success {
  color: var(--brand-success) !important;
}

.text-danger {
  color: var(--brand-danger) !important;
}

.text-muted {
  color: var(--muted-color) !important;
}


button {
  border-radius: 50px;
  background: transparent;
  padding: 8px 12px;
  box-shadow: 0 0 0 2px var(--brand-blue);
  border: none;
  cursor: pointer;

  &:hover {
    background: var(--brand-blue);
    color: white;
  }

  &.link {
    background: transparent;
    box-shadow: none;
    color: var(--brand-blue);
    padding: 0;
    margin: 0;
    font-size: 1rem;
    text-decoration: underline;
    cursor: pointer;
  }
}
</style>
