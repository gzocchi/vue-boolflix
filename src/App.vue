<template>
  <div id="app">
    <Header @filmSearch="headerSearch" />
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
    headerSearch(search) {
      this.search = search.results;
      console.log(this.search);
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
