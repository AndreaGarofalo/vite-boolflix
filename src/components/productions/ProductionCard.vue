<script>
export default {
  name: "Production Card",
  props: {
    item: Object,
  },
  computed: {
    title() {
      return this.item.title || this.item.name;
    },
    originalTitle() {
      return this.item.original_title || this.item.original_name;
    },
    hasFlag() {
      const flags = ["it", "en"];
      return flags.includes(this.item.original_language);
    },
    flagSrc() {
      const url = new URL(
        `../../assets/img/${this.item.original_language}.png`,
        import.meta.url
      );
      return url.href;
    },
  },
};
</script>

<template>
  <ul>
    <li>{{ item.title || item.name }}</li>
    <li>{{ item.original_title || item.original_name }}</li>
    <li>
      <img v-if="hasFlag" :src="flagSrc" :alt="item.original_language" />
      <div v-else>{{ item.original_language }}</div>
    </li>
    <li>{{ item.vote_average }}</li>
  </ul>
</template>

<style scoped lang="scss">
ul {
  list-style-type: none;
  li {
    img {
      height: 14px;
      width: 20px;
    }
  }
}
</style>
