<template>
  <main class="container py-3">
    <section id="row d-flex align-items-start gallery">
      <div
        class="col-12 col-sm-6 col-md-4 col-lg-3 d-inline-flex p-2 my-2 poster"
        v-for="(item, index) in searchArray"
        :key="index"
      >
        <Poster :item="item" />
      </div>
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
</style>
