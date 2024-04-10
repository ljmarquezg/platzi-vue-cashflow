<template>
  <div class="modal">
    <div class="head">
      <p>Nuevo Movimiento</p>
      <button
        class="link"
        @click="closeModal"
      >
        <span class="material-symbols-outlined">close</span>
      </button>
    </div>
    <div class="body">
      <slot></slot>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script setup>
import { defineEmits } from "vue";

const emit = defineEmits(["closeViewModalMovement"]);

const closeModal = () => emit("closeViewModalMovement");
</script>

<style
  lang="scss"
  scoped
>
.modal {
  z-index: 2;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: white;
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 24px 24px;
  box-sizing: border-box;
}

.body {
  display: flex;
  flex-direction: column;
  height: 90%;
}

p {
  margin: 0;
  font-size: 1.5rem;
  color: var(--brand-blue);
}
</style>
