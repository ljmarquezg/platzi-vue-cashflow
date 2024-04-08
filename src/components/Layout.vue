<template>
  <div class="header">
    <slot name="header"></slot>
  </div>
</template>

<script>
export default {
  name: "LayoutComponent"
};
</script>

<style lang="scss" scoped>
.header, .resume, .movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 14px;
}

.header {
  position: fixed;
  width: 100vw;
}

.movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 14px;

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
}
</style>
