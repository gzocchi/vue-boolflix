<template>
  <main class="container">
    <div class="poster" v-for="(item, index) in searchArray" :key="index">
      <ul>
        <li>Titolo: {{ item.title }}</li>
        <li>Titolo Originale: {{ item.original_title }}</li>
        <li>Lingua: {{ item.original_language }}</li>
        <li>Voto: {{ item.vote_average }}</li>
      </ul>
    </div>
  </main>
</template>

<script>
export default {
  name: "Main",
  props: ["searchArray"],
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

.poster {
  display: inline-block;
  width: calc(100% / 4);
  padding: 20px;
  border: 1px solid white;
}
ul {
  list-style: none;
  padding: 10px;
  background-color: rgba(255, 255, 255, 0.6);
}
</style>
