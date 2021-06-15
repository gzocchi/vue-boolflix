<template>
  <div id="app">
    <Header
      @searchMovieTv="multiSearch"
      @onlyMovie="singleSearch"
      @onlyTv="singleSearch"
    />
    <Main :searchArray="search" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data() {
    return {
      search: [],
    };
  },
  methods: {
    singleSearch(search, type) {
      this.search = search.results;
      this.search.forEach((element) => {
        element.media_type = type;
      });
      // DEBUG
      // console.log(this.search);
    },
    multiSearch(array) {
      this.search = array;
      // DEBUG
      // console.log(array);
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
