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
  text-align: center;
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
}
</style>
