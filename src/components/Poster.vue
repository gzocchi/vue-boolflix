<template>
  <div>
    <ul v-if="item.media_type == 'movie'">
      <li>Titolo: {{ item.title }}</li>
      <li>Titolo Originale: {{ item.original_title }}</li>
      <li v-if="item.original_language == 'en'">
        Lingua: <img class="flag" src="../assets/img/en.png" alt="en-EN" />
      </li>
      <li v-else-if="item.original_language == 'it'">
        Lingua: <img class="flag" src="../assets/img/it.png" alt="it-IT" />
      </li>
      <li v-else>
        Lingua: <span class="lang">{{ item.original_language }}</span>
      </li>
      <li>Voto: {{ vote }}</li>
    </ul>
    <ul v-else-if="item.media_type == 'tv'">
      <li>Titolo: {{ item.name }}</li>
      <li>Titolo Originale: {{ item.original_name }}</li>
      <li v-if="item.original_language == 'en'">
        Lingua: <img class="flag" src="../assets/img/en.png" alt="en-EN" />
      </li>
      <li v-else-if="item.original_language == 'it'">
        Lingua: <img class="flag" src="../assets/img/it.png" alt="it-IT" />
      </li>
      <li v-else>
        Lingua: <span class="lang">{{ item.original_language }}</span>
      </li>
      <li>Voto: {{ vote }}</li>
    </ul>
    <div class="poster_image">
          <img :src="imgUrl+imgDimension+item.poster_path" :alt="item.title" class="img-fluid">
      </div>
  </div>
</template>

<script>
export default {
  name: "Poster",
  props: ["item"],
  data() {
    return {
      vote: Math.round(this.item.vote_average) / 2,
      imgUrl: "https://image.tmdb.org/t/p",
      imgDimension: "/w342",
      fullStar: '<i class="fas fa-star"></i>',
      emptyStar: '<i class="far fa-star"></i>',
    };
  },
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

div {
  height: 100%;
  overflow: hidden;
  border: 1px solid white;
  background-color: rgba(255, 255, 255, 0.6);

  ul {
    list-style: none;
    padding: 10px;

    .flag {
      height: 15px;
    }
    .lang {
      text-transform: uppercase;
    }
  }
}
</style>
