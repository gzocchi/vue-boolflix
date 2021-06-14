<template>
  <main class="container py-3">
    <section id="row d-flex align-items-start gallery">
      <Poster
        v-for="(item, index) in searchArray"
        :key="index"
        :item="item"
        class="col-6 col-md-4 col-lg-3 d-inline-flex flex-column p-2 my-2 poster"
      />
    </section>
  </main>
</template>

<script>
import Poster from "./Poster.vue";
export default {
  name: "Main",
  components: {
    Poster,
  },
  props: ["searchArray"],
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

main {
  height: 100%;

  .poster {
      height: 60vh;
  }
}
</style>
