<template>
  <header class="container-fluid sticky-top">
    <div class="row align-items-center">
      <div
        class="logo d-flex justify-content-center col-12 col-sm-6 col-md-2 col-lg-3 "
      >
        <img src="../assets/img/logo.png" alt="Logo" />
      </div>
      <div
        class="search col-12 col-sm-6 col-md-6 offset-md-4 col-lg-4 offset-lg-5"
      >
        <div class="input-group">
          <input
            type="text"
            class="form-control"
            placeholder="Cerca film e serieTV ..."
            v-model.trim="query"
            @keydown.enter="multiSearch(query)"
          />
          <button
            class="btn btn-outline-secondary my_btn"
            type="button"
            @click="movieSearch(query)"
          >
            Film
          </button>
          <button
            class="btn btn-outline-secondary my_btn"
            type="button"
            @click="tvSearch(query)"
          >
            Serie TV
          </button>
        </div>
      </div>
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
        searchMulti: "https://api.themoviedb.org/3/search/multi",
        apiKey: "f83fba942aa33499ec38f009528f9e77",
        language: "it-IT",
      },
      query: "",
      currentSearch: "",
    };
  },
  methods: {
    movieSearch(query) {
      this.currentSearch = query;
      this.query = "";
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
        })
        .catch((error) => {
          console.log(error);
        });
    },
    tvSearch(query) {
      this.currentSearch = query;
      this.query = "";
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
        })
        .catch((error) => {
          console.log(error);
        });
    },
    multiSearch(query) {
      this.currentSearch = query;
      this.query = "";
      axios
        .get(this.api.searchMulti, {
          params: {
            api_key: this.api.apiKey,
            language: this.api.language,
            query,
          },
        })
        .then((res) => {
          this.$emit("search", res.data, false);
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
header {
  min-height: $header_h;
  background-color: grey;
  .row {
    height: 100%;
    .logo {
      height: 100%;
      img {
        height: 100%;
      }
    }
    .search {
      .my_btn {
        color: black;
        border-color: black;
        background-color: grey;
      }
    }
  }
}
</style>
