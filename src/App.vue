<template>
  <div id="app">
    <header>
      <app-search @performSearch="search" />
    </header>
    <main>
      <app-main :items="popularList" titolo="Popular" />
      <app-grid :items="filmList" :results="noResults" />
      <app-grid :items="serieList" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import AppSearch from "./components/AppSearch.vue";
import AppGrid from "./components/AppGrid.vue";
import AppMain from "./components/AppMain.vue";

export default {
  name: "App",
  components: {
    AppSearch,
    AppGrid,
    AppMain,
  },
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3/",
      apiKey: "f9f88b1e607ce852eb8d91625dc47ba1",
      filmList: [],
      serieList: [],
      popularList: [],
      noResults: false,
      title: true,
    };
  },
  methods: {
    cercaFilm(queryParams) {
      axios
        .get(this.apiUrl + "search/movie", queryParams)
        .then((res) => {
          this.filmList = res.data.results;
          this.popularList = "";
          if (this.filmList.length == 0 && this.serieList.length == 0) {
            this.noResults = true;
          } else {
            this.noResults = false;
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
    cercaSerie(queryParams) {
      axios
        .get(this.apiUrl + "search/tv", queryParams)
        .then((res) => {
          this.serieList = res.data.results;
          this.popularList = "";
          if (this.filmList.length == 0 && this.serieList.length == 0) {
            this.noResults = true;
          } else {
            this.noResults = false;
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },

    search(text) {
      const queryParams = {
        params: {
          api_key: this.apiKey,
          query: text,
        },
      };
      this.cercaFilm(queryParams);
      this.cercaSerie(queryParams);
    },
    cercaPopular() {
      axios
        .get(this.apiUrl + "movie/popular" + "?api_key=" + this.apiKey)
        .then((res) => {
          this.popularList = res.data.results;
          console.log(res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  created() {
    axios
      .get(this.apiUrl + "movie/popular" + "?api_key=" + this.apiKey)
      .then((res) => {
        this.popularList = res.data.results;
        console.log(res.data);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style lang="scss">
@import "./assets/style/general.scss";
</style>
