<template>
  <header class="container-fluid">
    <div class="input-group mb-3">
      <input
        type="text"
        class="form-control"
        placeholder="Ricerca Film"
        aria-label="Ricerca Film"
        aria-describedby="button-addon2"
        v-model.trim="query"
        @keyup.enter="filmSearch(query)"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
        @click="filmSearch(query)"
      >
        Cerca
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
    filmSearch(query) {
      axios
        .get(this.api.searchMovie, {
          params: {
            api_key: this.api.apiKey,
            language: this.api.language,
            query,
          },
        })
        .then((res) => {
          // console.log(res.data.results);
          // this.$emit("filmSearch", res.data.results);
          this.$emit("filmSearch", res.data);
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
