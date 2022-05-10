<template>
    <div>
        <input v-model="search" placeholder="Cerca un film" type="text">
        <button @click="cercaFilm" type="button">Cerca Film</button>
        
            <div v-for="film in filmList" :key="film">
                <p>{{'Titolo: '+film.title}}</p>
                <p>{{'Lingua: '+film.original_language}}</p>
                <p>{{'Voto: '+film.vote_average}}</p>
            </div>
        
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: "AppGrid",
    data(){
        return{
            apiUrl: 'https://api.themoviedb.org/3/search/',
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
                axios.get(this.apiUrl + "movie?", paramObj).then((res)=>{
                    this.filmList = res.data.results;
                })
                .catch((err)=>{
                    console.log(err)
                })
            }
    },
}
</script>

<style lang="scss" scoped>
button{
    color: black;
}
</style>