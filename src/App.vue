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
    };
  },
  methods: {
    headerSearch(search, type) {
      this.search = [search.results, type];
      // DEBUG
      console.log(this.search);
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
