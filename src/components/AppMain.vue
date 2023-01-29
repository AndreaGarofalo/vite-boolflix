<script>
import { store } from "../data/store";
import ProductionCard from "./productions/ProductionCard.vue";
export default {
  name: "Boolflix Main",
  components: { ProductionCard },
  data: () => ({ store, titleFilter: "" }),
};
</script>

<template>
  <main>
    <div class="container">
      <h2 class="text-light">Film</h2>
      <h2>Movies</h2>
      <section class="d-flex">
        <ProductionCard
          v-for="movie in store.movies"
          :key="movie.id"
          :item="movie"
        />
      </section>
      <h2>Series</h2>
      <section class="d-flex">
        <ProductionCard
          v-for="serie in store.series"
          :key="serie.id"
          :item="serie"
        />
      </section>
    </div>
  </main>
</template>

<style scoped lang="scss">
main {
  min-height: calc(100vh - 60px);
  background-color: #555555;
  margin-top: 60px;
  h2 {
    padding: 50px 0;
  }
  section {
    flex-wrap: wrap;
  }
}
</style>
