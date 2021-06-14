<template>
  <div id="app"></div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      api: {
        apiUrl: "https://api.themoviedb.org/3/search/movie",
        api_key: "f83fba942aa33499ec38f009528f9e77",
        language: "it-IT",
      },
    };
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
