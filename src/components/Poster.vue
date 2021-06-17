<template>
  <div
    class="poster_card"
    @mouseover="hover = true"
    @mouseleave="hover = false"
  >
    <div v-if="!hover" class="poster_image">
      <img
        :src="item.poster_path ? imageUrl : placeholder"
        :alt="item.title ? item.title : item.name"
      />
    </div>

    <div v-else class="poster_info p-3 m-0">
      <h3>{{ item.title ? item.title : item.name }}</h3>

      <ul class="p-0 m-0 fw-light">
        <li>
          <span class="fw-bold">Titolo Originale:</span>
          {{ item.original_title ? item.original_title : item.original_name }}
        </li>
        <li
          v-if="
            item.original_language == 'en' || item.original_language == 'it'
          "
        >
          <img
            :src="require(`../assets/img/${item.original_language}.png`)"
            :alt="`flag-${item.original_language}`"
            class="flag"
          />
        </li>
        <li v-else>
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
  props: {
    item: {
      type: Object,
      require: true,
    },
  },
  data() {
    return {
      imgUrl: "https://image.tmdb.org/t/p",
      imgDimension: "/w342",
      placeholder:
        "https://www.altavod.com/assets/images/poster-placeholder.png",
      // "https://www.2johnsrestaurant.com/wp-content/uploads/2014/06/placeholder_image1.png",
      // "http://www.premionapoli.it/wp-content/uploads/2015/10/pix-vertical-placeholder.jpg",
      hover: false,
      iso_3166_1: "",
    };
  },
  methods: {
    getCountriIso() {
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
    },
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
    this.getCountriIso();
  },
};
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";
@import "~flag-icon-css/css/flag-icon.css";

.poster_card {
  width: 100%;
  height: 450px;
  overflow: hidden;

  .poster_image {
    img {
      width: 100%;
      object-position: center;
      object-fit: cover;
    }
  }
  .poster_info {
    ul {
      list-style: none;

      .flag {
        height: 14px;
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
