<template>
  <main class="container py-3">
    <h2 v-if="searchArray.length == 0" class="text-center">
      Cerca Film e SerieTv
    </h2>

    <section
      id="row d-flex flex-row justify-content-start  align-items-start "
    >
      <div
        class="col-12 col-sm-6 col-md-4 col-lg-3 d-inline-flex p-2 my-2 gallery_card"
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

main {
  height: $main_h;
  overflow: auto;

}
</style>
