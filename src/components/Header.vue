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
            @keydown.enter="saerchMovieTv(query)"
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
        apiKey: "f83fba942aa33499ec38f009528f9e77",
        language: "it-IT",
      },
      query: "",
      currentSearch: "",
    };
  },
  methods: {
    saerchMovieTv(query) {
      this.currentSearch = query;

      let movie =
        "https://api.themoviedb.org/3/search/movie?api_key=f83fba942aa33499ec38f009528f9e77&language=it-IT&query=" +
        query;
      let tv =
        "https://api.themoviedb.org/3/search/tv?api_key=f83fba942aa33499ec38f009528f9e77&language=it-IT&query=" +
        query;

      const requestMovie = axios.get(movie);
      const requestTv = axios.get(tv);

      axios
        .all([requestMovie, requestTv])
        .then(
          axios.spread((...responses) => {
            const responseMovie = responses[0].data.results;
            const responseTv = responses[1].data.results;
            responseMovie.forEach((element) => {
              element.media_type = "movie";
            });
            responseTv.forEach((element) => {
              element.media_type = "tv";
            });
            this.$emit("searchMovieTv", [...responseMovie, ...responseTv]);
            this.query = "";
          })
        )
        .catch((error) => {
          console.err(error);
        });
    },
    movieSearch(query) {
      this.currentSearch = query;
      axios
        .get(this.api.searchMovie, {
          params: {
            api_key: this.api.apiKey,
            language: this.api.language,
            query,
          },
        })
        .then((res) => {
          this.singleData = res.data;
          this.$emit("onlyMovie", this.singleData, "movie");
          this.query = "";
        })
        .catch((error) => {
          console.log(error);
        });
    },
    tvSearch(query) {
      this.currentSearch = query;
      axios
        .get(this.api.searchTv, {
          params: {
            api_key: this.api.apiKey,
            language: this.api.language,
            query,
          },
        })
        .then((res) => {
          this.singleData = res.data;
          this.$emit("onlyTv", this.singleData, "tv");
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
