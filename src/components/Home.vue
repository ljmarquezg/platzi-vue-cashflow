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
          El grafico va aqui
        </template>

        <!-- Action section -->
        <template #action>
          <button @click="console.log('test')">Añadir movimiento</button>
        </template>
      </ResumeIndex>
    </template>

    <!-- Movements component -->
    <template #movements>
      <MovementsComponent
        :movements="movements"
      />
    </template>
  </LayoutComponent>
</template>

<script>
import LayoutComponent from "@/components/LayoutComponent.vue";
import HeaderComponent from "@/components/Header.vue";
import ResumeIndex from "@/components/Resume/ResumeIndex.vue";
import MovementsComponent from "@/components/Movements/MovementsIndex.vue";

export default {
  name: "HomeComponent",
  components: {
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
          id: '0003',
          date: '2023-03-01',
          title: 'Ingreso de nómina',
          description: 'Ingreso de nómina mes de marzo',
          amount: 2000
        },
        {
          id: '0004',
          date: '2023-04-01',
          title: 'Ingreso de nómina',
          description: 'Ingreso de nómina mes de abril',
          amount: -150
        },
        {
          id: '0003',
          date: '2023-05-01',
          title: 'Ingreso de nómina',
          description: 'Ingreso de nómina mes de mayo',
          amount: -500
        },
        {
          id: '0006',
          date: '2021-06-01',
          title: 'Ingreso de nómina',
          description: 'Ingreso de nómina mes de junio',
          amount: -900
        }
      ]
    };
  }
};
</script>

<style
  lang="scss"
  scoped
>

</style>
