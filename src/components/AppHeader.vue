<script>
import axios from "axios";
import SearchBar from "./SearchBar.vue";
import { api } from "../data";
import { store } from "../data/store";
export default {
  name: "Boolflix Header",
  components: { SearchBar },
  data: () => ({ store, titleFilter: "" }),
  computed: {
    axiosConfig() {
      const { key, language } = api;
      return {
        params: {
          language,
          api_key: key,
          query: this.titleFilter,
        },
      };
    },
  },
  methods: {
    updateTitleFilter(term) {
      this.titleFilter = term;
    },
    searchProductions() {
      if (!this.titleFilter) {
        store.movies = [];
        store.series = [];
        return;
      }
      this.fetchApi("search/movie", "movies");
      this.fetchApi("search/tv", "series");
    },
    fetchApi(endpoint, collection) {
      axios
        .get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
        .then((res) => {
          store[collection] = res.data.results;
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>

<template>
  <header>
    <div class="container">
      <div class="header-content">
        <h2>BOOLFLIX</h2>
        <SearchBar
          @term-change="updateTitleFilter"
          placeholder="Cerca un film"
          @form-submit="searchProductions"
        />
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
header {
  background-color: black;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
  .container {
    height: 100%;
    .header-content {
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      h2 {
        color: red;
      }
    }
  }
}
</style>
