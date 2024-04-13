<template>
  <div>
    <button
      class="filled"
      @click="openModal"
    >
      Agregar Movimiento
    </button>

    <teleport to="#app">
      <ModalView
        @closeViewModalMovement="closeModal"
        v-show="showModal"
      >
        <FormComponent
          @closeViewModalMovement="closeModal"
          @create="create"
        />
      </ModalView>
    </teleport>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";
import ModalView from "@/components/ModalView.vue";
import FormComponent from "@/components/FormComponent.vue";
const emit = defineEmits(["updateMovements"]);
const showModal = ref(false);
const openModal = () => {
  showModal.value = true;
};
const closeModal = () => {
  showModal.value = false;
};
const create = (data) => {
  emit('updateMovements', data);
  closeModal();
}
</script>

<style scoped>


</style>
