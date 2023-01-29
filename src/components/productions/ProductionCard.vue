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
    buildImageUrl() {
      const imageUrl = `https://image.tmdb.org/t/p/w342${this.item.poster_path}`;
      return imageUrl;
    },
  },
};
</script>

<template>
  <ul>
    <li>
      <img :src="buildImageUrl" :alt="this.title" />
    </li>
    <li>{{ this.title }}</li>
    <li>{{ this.originalTitle }}</li>
    <li>
      <img
        class="flag"
        v-if="hasFlag"
        :src="flagSrc"
        :alt="item.original_language"
      />
      <div v-else>{{ item.original_language }}</div>
    </li>
    <li>{{ item.vote_average }}</li>
  </ul>
</template>

<style scoped lang="scss">
ul {
  list-style-type: none;
  li {
    .flag {
      height: 14px;
      width: 20px;
    }
  }
}
</style>
