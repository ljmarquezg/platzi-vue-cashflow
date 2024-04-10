<template>
  <form @submit.prevent="addMovement">
    <!-- Title Field -->
    <div class="field">
      <label for="title">Título</label>
      <input
        type="text"
        id="title"
        v-model="title"
      />
    </div>

    <!-- Amount Field -->
    <div class="field">
      <label for="title">Monto</label>
      <input
        id="title"
        type="number"
        v-model="amount"
        class="text-right"
      />
    </div>

    <!-- Description Field -->
    <div class="field">
      <label for="title">Description</label>
      <textarea
        row="4"
        id="description"
        v-model="description"
      />
    </div>

    <!-- Movement Type Field -->
    <div class="field">
      <label
        class="radio-label"
        for="ingreso"
      >
        <input
          type="radio"
          id="ingreso"
          v-model="movementsType"
          value="Ingreso"
        />
        <span>Ingreso</span>
      </label>

      <label
        class="radio-label"
        for="gasto"
      >
        <input
          type="radio"
          id="gasto"
          v-model="movementsType"
          value="Gasto"
        />
        <span>Gasto</span>
      </label>
    </div>

    <div class="actions">
      <button
        class="filled"
        type="submit"
      >
        Agregar Movimiento
      </button>

      <button
        type="button"
        @click="closeModal"
      >
        Cancelar
      </button>
    </div>
  </form>
</template>

<script setup>
import { defineEmits, ref } from "vue";

const emit = defineEmits(["closeViewModalMovement"]);
// Form Inputs
const title = ref("");
const amount = ref(0);
const description = ref("");
const movementsType = ref("Ingreso");

const addMovement = () => {
  console.log("addMovement");
  closeModal();
};

const closeModal = () => emit("closeViewModalMovement");

</script>

<style
  lang="scss"
  scoped
>

form {
  height: 100%;
  padding: 1rem;
  display: flex;
  flex-direction: column;
}

.field {
  margin-bottom: 1rem;

  label {
    display: block;
    margin-bottom: 0.5rem;
  }

  input, textarea {
    width: 100%;
    padding: 0.5rem;
    border: 2px solid var(--border-color);
    border-radius: 4px;
  }
}

.radio-label {
  display: flex;
  align-items: center;
  margin-right: 1rem;

  input {
    width: auto;
    margin-right: 0.5rem;
  }
}

.actions {
  flex: auto;
  display: flex;
  height: auto;
  justify-content: flex-end;
  align-items: flex-end;
  flex-direction: column;
}

button {
  min-width: 100%;
  margin-bottom: 1rem;
}

</style>
