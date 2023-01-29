<script>
import { api } from "./data";
import { store } from "./data/store";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
export default {
  name: "Boolflix",
  components: { AppHeader, AppMain },
  data: () => ({ store }),
};
</script>

<template>
  <AppHeader />
  <AppMain />
</template>

<style></style>
