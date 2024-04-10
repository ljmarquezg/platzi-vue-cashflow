<template>
  <!-- Header Slot -->
  <div class="header">
    <slot name="header"></slot>
  </div>

  <!-- Resume Slot -->
  <div class="resume">
    <slot name="resume"></slot>
  </div>

  <!-- Movements Slot -->
  <div class="movements">
    <div class="head" @click="showMovements = !showMovements">
      <div class="grip"></div>
    </div>

    <div class="body" v-show="showMovements">
      <slot name="movements"></slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showMovements = ref(false);
</script>

<style
  lang="scss"
  scoped
>
.header, .resume, .movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 14px;
}

.header {
  position: fixed;
  width: 100vw;
  top: 0;
  left: 0;
}

.resume {
  min-height: 100vh;
}


.movements {
  z-index: 1;
  position: absolute;
  flex-direction: column;
  bottom: 0;
  width: 100vw;
  background-color: white;
  box-shadow: 0 -8px 16px var(--light-background-color);
  border-radius: 24px;

  .head {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 24px;
    width: 100%;

    .grip {
      width: 120px;
      height: 8px;
      background-color: #e5e5e5;
      border-radius: 4px;
    }
  }

  .body {
    height: 75vh;
    width: 100%;
  }
}
</style>
