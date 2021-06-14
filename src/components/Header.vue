<template>
  <header class="container-fluid">
    <!-- <div class="input-group mb-3">
      <input
        type="text"
        class="form-control"
        placeholder="Ricerca Film"
        aria-label="Ricerca Film"
        aria-describedby="button-addon2"
        v-model.trim="query"
        @keyup.enter="movieSearch(query)"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
        @click="movieSearch(query)"
      >
        Cerca
      </button>
    </div> -->

    <div class="input-group">
      <input
        type="text"
        class="form-control"
        placeholder="Ricerca ..."
        v-model.trim="query"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        @click="movieSearch(query)"
      >
        Film
      </button>
      <button
        class="btn btn-outline-secondary"
        type="button"
        @click="tvSearch(query)"
      >
        Serie TV
      </button>
    </div>
  </header>
</template>

<script>
import axios from "axios";

export default {
  name: "Header",
  data() {
    return {
      api: {
        searchMovie: "https://api.themoviedb.org/3/search/movie",
        searchTv: "https://api.themoviedb.org/3/search/tv",
        apiKey: "f83fba942aa33499ec38f009528f9e77",
        language: "it-IT",
      },
      query: "",
    };
  },
  methods: {
    movieSearch(query) {
      axios
        .get(this.api.searchMovie, {
          params: {
            api_key: this.api.apiKey,
            language: this.api.language,
            query,
          },
        })
        .then((res) => {
          this.$emit("search", res.data, "movie");
          this.query = "";
        })
        .catch((error) => {
          console.log(error);
        });
    },
    tvSearch(query) {
      axios
        .get(this.api.searchTv, {
          params: {
            api_key: this.api.apiKey,
            language: this.api.language,
            query,
          },
        })
        .then((res) => {
          this.$emit("search", res.data, "tv");
          this.query = "";
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";
div {
  height: $header_h;
  background-color: #fff;
}
</style>
