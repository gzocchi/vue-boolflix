<template>
  <div id="app">
    <Header @search="headerSearch" />
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
      page: "",
      total_page: "",
      total_result: "",
    };
  },
  methods: {
    headerSearch(search, type) {
      this.page = search.page;
      this.total_page = search.total_pages;
      this.total_result = search.total_results;
      this.search = search.results;
      this.search.forEach((element) => {
        // if (type == "movie") {
        //   element.media_type = "movie";
        // }
        // if (type == "tv") {
        //   element.media_type = "tv";
        // }
        if (type) {
          element.media_type = type;
        }
      });
      // DEBUG
      console.log(this.search);
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
