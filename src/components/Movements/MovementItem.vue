<template>
  <li
    class="movement-item"
    :id="id"
  >
    <!-- Movement Item Header -->
    <div class="movement-item__header">
      <div class="movement-item__date">
        {{ date }}
      </div>
      <button
        class="link text-muted"
        @click="removeItem"
      >
        <span class="material-symbols-outlined">delete</span>
      </button>
    </div>

    <!-- Movement Item Content -->
    <div class="movement-item__content">
      <!-- Movement Item Date -->
      <div class="movement-item__info">
        <h3 class="movement-item__title">{{ title }}</h3>
        <p
          v-if="description"
          class="movement-item__description"
        >
          {{ description }}
        </p>
      </div>
      <!-- Movement Item Amount -->
      <strong
        class="movement-item__amount"
        :class="amount < 0 ? 'text-danger' : 'text-success'"
      >
        <CurrencyFormatComponent :amount="amount" />
      </strong>
    </div>
  </li>
</template>

<script setup>
import { defineProps, toRefs, defineEmits } from "vue";
import MovementsDefinition from "@/components/Movements/MovementsDefinition";
import CurrencyFormatComponent from "@/components/shared/CurrencyFormatComponent.vue";

const props = defineProps({
  movement: {
    type: MovementsDefinition,
    default: () => {
    }
  }
});

const { id, title, date, description, amount } = toRefs(props.movement);
const emit = defineEmits(["removeItem"]);

const removeItem = () => {
  emit("removeItem", id.value);
};
</script>

<style
  lang="scss"
  scoped
>
:root {
  --item-padding: 0 16px;
}

.movement-item {
  display: flex;
  flex-direction: column;
  background: white;
  border-radius: 5px;
  padding: 16px;
  box-shadow: var(--box-shadow);
}

.movement-item__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 8px;
}

.movement-item__date {
  font-size: .85rem;
  padding: 4px 8px;
}

.movement-item__content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 4px 8px;
}

.movement-item__title {
  margin: 0;
  color: var(--brand-blue);
}

.movement-item__description {
  margin: 0;
  font-size: .85rem;
}
</style>
