<template>
  <div
    class="poster_card"
    @mouseover="hover = true"
    @mouseleave="hover = false"
  >
    <div v-if="!hover" class="poster_image">
      <img :src="item.poster_path ? imageUrl : placeholder" :alt="item.title" />
    </div>

    <div v-else class="poster_info p-3 m-0">
      <h3>{{ item.title ? item.title : item.name }}</h3>

      <ul class="p-0 m-0 fw-light">
        <li>
          <span class="fw-bold">Titolo Originale:</span>
          {{ item.original_title ? item.original_title : item.original_name }}
        </li>
        <li>
          <span class="flag-icon" :class="`flag-icon-${iso_3166_1}`"></span>
        </li>
        <li>
          <i
            v-for="number in 5"
            :key="number"
            class="fa-star p-0 m-0"
            :class="number <= vote ? 'fas' : 'far'"
          ></i>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Poster",
  props: ["item"],
  data() {
    return {
      imgUrl: "https://image.tmdb.org/t/p",
      imgDimension: "/w342",
      placeholder:
        "http://www.premionapoli.it/wp-content/uploads/2015/10/pix-vertical-placeholder.jpg",
      hover: false,
      iso_3166_1: "",
    };
  },
  computed: {
    imageUrl() {
      return this.imgUrl + this.imgDimension + this.item.poster_path;
    },
    vote() {
      return Math.round(this.item.vote_average / 2);
    },
  },
  created() {
    if (this.item.original_language == "en") {
      this.iso_3166_1 = "gb";
    }
    if (this.item.original_language == "it") {
      this.iso_3166_1 = "it";
    } else {
      axios
        .get(
          `https://api.themoviedb.org/3/${this.item.media_type}/${this.item.id}`,
          {
            params: {
              api_key: "f83fba942aa33499ec38f009528f9e77",
            },
          }
        )
        .then((res) => {
          res.data.production_countries.length > 0
            ? (this.iso_3166_1 = res.data.production_countries[0].iso_3166_1.toLowerCase())
            : (this.iso_3166_1 = this.item.original_language);
        })
        .catch((error) => {
          console.log(error);
        });
    }
  },
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";
@import "~flag-icon-css/css/flag-icon.css";

.poster_card {
  width: 100%;
  height: 400px;
  overflow: hidden;
  border: 1px solid white;

  .poster_image {
    img {
      // height: 100%;
      width: 100%;
      object-position: center;
      object-fit: cover;
    }
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
}
</style>
