<template>
  <div>
    <h1>Actions</h1>
    <button @click="openModal">Agregar Movimiento</button>

    <teleport to="#app">
      <ModalView
        @closeViewModalMovement="closeModal"
        v-show="showModal"
      >
        <FormComponent @closeViewModalMovement="closeModal"/>
      </ModalView>
    </teleport>
  </div>
</template>

<script setup>
import { ref } from "vue";
import ModalView from "@/components/ModalView.vue";
import FormComponent from "@/components/FormComponent.vue";

const showModal = ref(false);
const openModal = () => {
  showModal.value = true;
};
const closeModal = () => {
  showModal.value = false;
};
</script>

<style scoped>


</style>
