<template>
  <div id="app"></div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      api: {
        searchMovie: "https://api.themoviedb.org/3/search/movie",
        searchTv: "https://api.themoviedb.org/3/search/tv",
        apiKey: "f83fba942aa33499ec38f009528f9e77",
        language: "it-IT",
      },
    };
  },
  created() {
    axios
      .get(this.api.searchMovie, {
        params: {
          api_key: this.api.apiKey,
          language: this.api.language,
          query: "ritorno al futuro",
        },
      })
      .then(function(res) {
        console.log(res.data.results);
      })
      .catch(function(error) {
        console.log(error);
      });
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
