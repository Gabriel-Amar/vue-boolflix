<template>
    <section>
        <div class="titolo">
            {{title}}
        </div>
        <div class="cerca">
            <div v-for="item in items" :key="item.id">
                <p>Titolo: {{item.title ? item.title : item.name}}</p>
                <p>Titolo originale: {{item.original_title ? item.original_title : item.original_name}}</p>
                <p>Lingua: <country-flag :country='FilmLanguage(item)' size='normal'/></p>
                <p>Voto: {{item.vote_average}}</p>
                <img class="img-fluid" :src="image + item.poster_path" alt="">
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: 'GridList',
    props:{
        items: Array,
        title: String
    },
    data(){
        return {
            image:'https://image.tmdb.org/t/p/w342'
        }
    },
    methods:{
        FilmLanguage(film){
                        if(film.original_language === 'en'){
                            return film.original_language = 'gb'
                        }else if(film.original_language === 'ja'){
                            return film.original_language = 'jp'
                        }else{
                            return film.original_language
                        }
                    },
    }
}
</script>

<style lang="scss">
</style>