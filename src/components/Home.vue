<template>
  <LayoutComponent>
    <template #header>
      <HeaderComponent />
    </template>
  </LayoutComponent>
</template>

<script>
import LayoutComponent from "@/components/Layout.vue";
import HeaderComponent from "@/components/Header.vue";

export default {
  name: "HomeComponent",
  components: {
    LayoutComponent,
    HeaderComponent
  }
};
</script>

<style
  lang="scss"
  scoped
>

</style>
