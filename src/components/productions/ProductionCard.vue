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
    roundVote() {
      const vote = Math.round(Math.round(this.item.vote_average) / 2);
      return vote;
    },
    voteToFive() {
      const voteToFive = 5 - this.roundVote;
      return voteToFive;
    },
  },
};
</script>

<template>
  <ul v-if="this.item.poster_path">
    <li class="poster">
      <img class="logo" :src="buildImageUrl" :alt="this.title" />
      <ul class="description">
        <li>
          <span> Titolo: </span>
          {{ this.title }}
        </li>
        <li>
          <span> Titolo originale: </span>
          {{ this.originalTitle }}
        </li>
        <li>
          <span> Lingua: </span>
          <img
            class="flag"
            v-if="hasFlag"
            :src="flagSrc"
            :alt="item.original_language"
          />
          <div v-else>{{ item.original_language }}</div>
        </li>
        <li>
          <span> Voto: </span>
          <i
            v-if="this.roundVote"
            v-for="fullStar in this.roundVote"
            :key="fullStar"
            class="fa-solid fa-star"
          ></i>
          <i
            v-if="this.voteToFive"
            v-for="emptyStar in this.voteToFive"
            :key="emptyStar"
            class="fa-regular fa-star"
          ></i>
        </li>
        <li v-if="item.overview">
          <span>Overview:</span>
          {{ item.overview }}
        </li>
      </ul>
    </li>
  </ul>
</template>

<style scoped lang="scss">
ul {
  list-style-type: none;
  .poster {
    height: 513px;
    .logo {
      width: 342px;
      height: 100%;
    }

    .description {
      background-color: rgba(54, 54, 54, 0.555);
      display: none;
      font-size: 16px;
      color: rgb(119, 119, 119);
      padding: 20px;
      span {
        font-size: 18px;
        color: white;
      }

      .flag {
        height: 20px;
        width: 30px;
      }
    }
  }
  .poster:hover .logo {
    display: none;
  }
  .poster:hover .description {
    display: block;
    width: 342px;
    height: 513px;
  }
}
.fa-star {
  color: yellow;
}
</style>
