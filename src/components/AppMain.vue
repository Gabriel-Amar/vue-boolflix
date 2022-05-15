<template>
  <section>
    <div class="container-fluid">
      <div class="row">
        <h1 v-if="items">{{ titolo }}</h1>
        <h1 v-else></h1>
        <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2" v-for="item in items" :key="item.id">
          <div class="product-image">
            <img
              v-if="item.poster_path"
              class="img-fluid"
              :src="img + item.poster_path"
              alt=""
            />
            <img
              class="img-fluid"
              v-else
              src="../assets/nt0ii3ns2zc29vwuqbug.jpg"
              alt=""
            />
            <div class="info">
              <h5 class="text-center">{{ item.title }}</h5>
              <div>
                <strong>Titolo originale: </strong>{{ item.original_title }}
              </div>
              <div class="d-flex">
                <strong>Lingua: </strong
                ><country-flag
                  class="mx-1"
                  :country="FilmLanguage(item)"
                  size=""
                />
              </div>
              <span v-for="(n, index) in 5" :key="index">
                <span
                  :class="
                    n <= transformScale(item)
                      ? 'fa-solid fa-star'
                      : 'fa-regular fa-star'
                  "
                ></span>
              </span>
              <div><strong>Trama: </strong>{{ item.overview }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "AppMain",
  props: {
    items: Array,
    titolo: String,
  },
  data() {
    return {
      img: "https://image.tmdb.org/t/p/w342",
    };
  },
  methods: {
    FilmLanguage(film) {
      if (film.original_language === "en") {
        return "gb";
      } else if (film.original_language === "ja") {
        return "jp";
      } else {
        return film.original_language;
      }
    },
    transformScale(film) {
      return Math.round(film.vote_average / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
.info {
  overflow-y: auto;
}
.info::-webkit-scrollbar {
  width: 3px;
}
h1 {
  color: whitesmoke;
}
.fa-solid {
  color: #ffbd00;
}
div.d-flex > span {
  margin-top: -2px;
}
.product-image {
  transition: all 0.3s ease-out;
  position: relative;
  overflow: hidden;
  display: inline-block;
  margin: 40px;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 19px 38px,
    rgba(0, 0, 0, 0.22) 0px 15px 12px;
}
.info {
  background: rgba(27, 26, 26, 0.9);
  transition: all 0.3s ease-out;
  transform: translateX(-100%);
  position: absolute;
  line-height: 1.8;
  text-align: left;
  font-size: 105%;
  cursor: pointer;
  color: #fff;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
  padding: 15px;
}
.info h2 {
  text-align: center;
}
.product-image:hover .info {
  transform: translateX(0);
}
.info div {
  transition: 0.3s ease;
}
.product-image:hover img {
  transition: all 0.3s ease-out;
  animation: kenburns-top 0.5s ease-out both;
}
@keyframes kenburns-top {
  0% {
    transform: scale(1) translateY(0);
    transform-origin: 50% 16%;
  }
  100% {
    transform: scale(1.25) translateY(-15px);
    transform-origin: top;
  }
}
</style>