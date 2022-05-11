<template>
  <div id="app">
    <header>
      <app-search @performSearch="search"/>
    </header>
    <main>
      <app-grid :items="filmList" title="Film"/>
      <app-grid :items="serieList" title="Serie"/>
    </main>
  </div>
</template>

<script>
import AppSearch from './components/AppSearch.vue'
import axios from "axios"
import AppGrid from './components/AppGrid.vue'




export default {
  name: 'App',
  components: {
    AppSearch,
    AppGrid
  },
  data(){
    return{
            apiUrl: 'https://api.themoviedb.org/3/search/',
            apiKey: "f9f88b1e607ce852eb8d91625dc47ba1",
            filmList: [],
            serieList: [],
    }
  },
  methods:{ 
            cercaFilm(queryParams){
                
                axios.get(this.apiUrl + "movie", queryParams).then((res)=>{
                    this.filmList = res.data.results;
                })
                .catch((err)=>{
                    console.log(err)
                })
            },
            cercaSerie(queryParams){
                
                axios.get(this.apiUrl + "tv", queryParams).then((res)=>{
                    this.serieList = res.data.results;
                })
                .catch((err)=>{
                    console.log(err)
                })
            },
            search(text){
              const queryParams = {
                params: {
                  api_key: this.apiKey,
                  query: text
                }
              }
              this.cercaFilm(queryParams)
              this.cercaSerie(queryParams)
            }
            
            
  }
}
</script>

<style lang="scss">
@import "./assets/style/general.scss";


</style>
