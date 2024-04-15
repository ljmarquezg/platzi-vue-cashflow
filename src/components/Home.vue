<template>
  <LayoutComponent>
    <!-- Header component -->
    <template #header>
      <HeaderComponent />
    </template>

    <!-- Resume component -->
    <template #resume>
      <ResumeIndex
        :label="'Ahorro total'"
        :amount="amount"
        :total-amount="totalAmount"
      >
        <!-- Graphic section -->
        <template #graphic>
          <GraphicComponent
            :amounts="amounts"
            @select="select"
          />
        </template>

        <!-- Action section -->
        <template #action>
          <ActionComponent
            @updateMovements="updateMovements"
          />
        </template>
      </ResumeIndex>
    </template>

    <!-- Movements component -->
    <template #movements>
      <MovementsComponent
        :movements="movements"
        @removeItem="removeItem"
      />
    </template>
  </LayoutComponent>
</template>

<script>
import LayoutComponent from "@/components/LayoutComponent.vue";
import HeaderComponent from "@/components/Header.vue";
import ResumeIndex from "@/components/Resume/ResumeIndex.vue";
import MovementsComponent from "@/components/Movements/MovementsIndex.vue";
import ActionComponent from "@/components/ActionComponent.vue";
import GraphicComponent from "@/components/Resume/GraphicComponent.vue";

export default {
  name: "HomeComponent",
  components: {
    GraphicComponent,
    ActionComponent,
    LayoutComponent,
    HeaderComponent,
    ResumeIndex,
    MovementsComponent
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: []
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
      .filter(movement => {
        const today = new Date();
        const oldDate = today.setDate(today.getDate() - 30);
        return movement.time > oldDate;
      })
      .map(filteredMovements => filteredMovements.amount);

      return lastDays.map((movement, index) => {
        const lastMovements = lastDays.slice(0, index + 1);

        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, movement) => {
        return suma + movement.amount;
      }, 0);
    }
  },
  methods: {
    updateMovements(movement) {
      this.movements.push(movement);
      this.save();
    },
    removeItem(id) {
      this.movements = this.movements.filter(movement => movement.id !== id);
      this.save();
    },
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
    select(value){
      this.amount = value;
    }
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));

    if (Array.isArray(movements)) {
      this.movements = movements.map(movement => {
        return { ...movement, time: new Date(movement.time) };
      });
    }
  }
};
</script>

<style
  lang="scss"
  scoped
>

</style>
