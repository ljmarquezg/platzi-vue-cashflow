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
        :total-amount="1000000"
      >
        <!-- Graphic section -->
        <template #graphic>
          <GraphicComponent
            :amounts="amounts"
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
      movements: [
        {
          id: "0003",
          time: new Date("2024-04-01"),
          title: "Ingreso de nómina",
          description: "Ingreso de nómina mes de marzo",
          amount: 100
        },
        {
          id: "0004",
          time: new Date("2024-04-02"),
          title: "Ingreso de nómina",
          description: "Ingreso de nómina mes de abril",
          amount: 100
        },
        {
          id: "0003",
          time: new Date("2024-04-03"),
          title: "Ingreso de nómina",
          description: "Ingreso de nómina mes de mayo",
          amount: -100
        },
        {
          id: "0006",
          time: new Date("2024-04-03"),
          title: "Ingreso de nómina",
          description: "Ingreso de nómina mes de junio",
          amount: 100
        }
      ]
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
    }
  },
  methods: {
    updateMovements(movement) {
      this.movements.push(movement);
    },
    removeItem(id) {
      this.movements = this.movements.filter(movement => movement.id !== id);
    }
  }
};
</script>

<style
  lang="scss"
  scoped
>

</style>
