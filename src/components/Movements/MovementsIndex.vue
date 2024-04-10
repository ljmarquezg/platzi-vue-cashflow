<template>
  <div class="movements">
    <!-- Title -->
    <h2 class="title">Historial</h2>

    <!-- Content -->
    <ul class="content">
        <MovementItem
          v-for="movement in movements"
          :movement="movement"
          :key="movement.id"
          @removeItem="removeItem"
        />
    </ul>
  </div>
</template>

<script setup>
import { defineProps, toRefs } from "vue";
import MovementItem from "@/components/Movements/MovementItem.vue";
import MovementsDefinition from "@/components/Movements/MovementsDefinition";

const props = defineProps({
  movements: {
    type: [MovementsDefinition],
    default: () => []
  }
});

const { movements } = toRefs(props);
const removeItem = (id) => {
  console.log(id);
};

</script>


<style
  lang="scss"
  scoped
>
.movements {
  max-height: 100%;
  margin-bottom: 14px;
}

.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}

.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 20px;
  overflow-y: scroll;
  padding: 12px;
}

</style>
