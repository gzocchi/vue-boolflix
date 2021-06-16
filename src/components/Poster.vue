<template>
  <div
    class="poster_card"
    @mouseover="hover = true"
    @mouseleave="hover = false"
  >
    <div v-if="!hover && item.poster_path" class="poster_image">
      <img
        :src="
          item.poster_path
            ? imgUrl + imgDimension + item.poster_path
            : placeholder
        "
        :alt="item.title"
      />
    </div>

    <div v-else class="poster_info p-2 m-0">
      <h3>{{ item.title ? item.title : item.name }}</h3>

      <ul class="p-0 m-0 fw-light">
        <li>
          <span class="fw-bold">Titolo Originale:</span>
          {{ item.original_title ? item.original_title : item.original_name }}
        </li>
        <li v-if="item.original_language == 'en'">
          <span class="fw-bold">Lingua: </span
          ><img class="flag" src="../assets/img/en.png" alt="en-EN" />
        </li>
        <li v-else-if="item.original_language == 'it'">
          <span class="fw-bold">Lingua: </span
          ><img class="flag" src="../assets/img/it.png" alt="it-IT" />
        </li>
        <li v-else>
          <span class="fw-bold">Lingua: </span>
          <span class="lang text-uppercase">{{ item.original_language }}</span>
        </li>
        <li>
          <i
            v-for="number in 5"
            :key="number"
            class="fa-star p-0 m-0"
            :class="number <= vote ? fullStar : emptyStar"
          ></i>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Poster",
  props: ["item"],
  data() {
    return {
      vote: Math.round(this.item.vote_average / 2),
      imgUrl: "https://image.tmdb.org/t/p",
      imgDimension: "/w342",
      fullStar: "fas",
      emptyStar: "far",
      placeholder:
        "http://www.premionapoli.it/wp-content/uploads/2015/10/pix-vertical-placeholder.jpg",
      hover: false,
    };
  },
  computed: {
    imageUrl() {
      return this.imgUrl + this.imgDimension + this.item.poster_path;
    },
  },
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

.poster_card {
  width: 100%;
  max-height: 400px;
  overflow: hidden;
  border: 1px solid white;
  // background-color: rgba(255, 255, 255, 0.6);

  // .poster_info,
  .poster_image {
    width: 100%;
    height: 100%;
    
  }
  .poster_image.hover{
    opacity: 0.1;
  }
  .poster_info {
    ul {
      list-style: none;

      .flag {
        height: 15px;
      }

      i.fas {
        color: gold;
      }
      i.far {
        color: white;
      }
    }
  }
  .poster_image {
    img {
      height: 100%;
      width: 100%;
      object-position: center;
      object-fit: cover;
    }
  }
}
</style>
