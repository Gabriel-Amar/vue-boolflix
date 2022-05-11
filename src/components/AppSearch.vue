<template>
    <div>
        <div class="titolo">
            <h1>Boolflix</h1>
        </div>
        <div class="cerca">
            <input v-model="search" placeholder="Cerca un film" type="text">
            <button @click="cercaFilm" type="button" class="btn btn-primary">Cerca Film</button>
            <div v-for="film in filmList" :key="film">
                <p>{{'Titolo: '+ film.title}}</p>
                <p>{{'Titolo originale: '+ film.original_title}}</p>
                <p>{{'Lingua: '+ film.original_language}}</p>
                <p>{{'Voto: '+ film.vote_average}}</p>
            </div>
        </div>
        
        
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: "AppSearch",
    data(){
        return{
            apiUrl: 'https://api.themoviedb.org/3/',
            apiKey: "f9f88b1e607ce852eb8d91625dc47ba1",
            filmList: [],
            search:"",
        }
    },
    methods:{
        cercaFilm(){
            const paramObj = {
                params: {
                    api_key: this.apiKey,
                    query: this.search,
                    
                }
            }
                axios.get(this.apiUrl + "search/movie", paramObj).then((res)=>{
                    this.filmList = res.data.results;
                })
                .catch((err)=>{
                    console.log(err)
                })
            }
    },
    computed:{
        
    }
}
</script>

<style lang="scss">
@import "../assets/style/general.scss";


button{
    color: black;
}
</style>