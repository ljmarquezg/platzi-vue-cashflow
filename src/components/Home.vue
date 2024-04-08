<template>
  <LayoutComponent>
    <!-- Header component -->
    <template #header>
      <HeaderComponent />
    </template>

    <!-- Resume component -->
    <template #resume>
      <ResumeComponent />
    </template>

    <!-- Movements component -->
    <template #movements>
      <MovementsComponent />
    </template>
  </LayoutComponent>
</template>

<script>
import LayoutComponent from "@/components/LayoutComponent.vue";
import HeaderComponent from "@/components/Header.vue";
import ResumeComponent from "@/components/Resume/Index.vue";
import MovementsComponent from "@/components/Moments.vue";

export default {
  name: "HomeComponent",
  components: {
    LayoutComponent,
    HeaderComponent,
    ResumeComponent,
    MovementsComponent
  }
};
</script>

<style
  lang="scss"
  scoped
>

</style>
