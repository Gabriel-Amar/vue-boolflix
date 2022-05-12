<template>
    <section>
        <!-- <div class="titolo">
            {{title}}
        </div> -->
        <div class="container-fluid">
            <div class="row">
            <div class="col-2" v-for="item in items" :key="item.id">
                <div class="product-image">
                    <img v-if="item.poster_path" class="img-fluid" :src="image + item.poster_path" alt="">
                    <img class="img-fluid" v-else src="../assets/nt0ii3ns2zc29vwuqbug.jpg" alt="">
                    <div class="info">
                        <h5 class="text-center">{{item.title ? item.title : item.name}}</h5>
                            <div>Titolo originale: {{item.original_title ? item.original_title : item.original_name}}</div>
                            <div class="d-flex">Lingua: <country-flag :country='FilmLanguage(item)' size='normal'/></div>
                            <span v-for="(n,index) in 5" :key="index">
                                <span :class="n <= transformScale(item) ? 'fa-solid fa-star' : 'fa-regular fa-star'"></span>
                            </span>
                            <div>Trama: {{item.overview}}</div>
                    </div>
                </div>
            </div>
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
                            return 'gb'
                        }else if(film.original_language === 'ja'){
                            return 'jp'
                        }else{
                            return film.original_language
                        }
                    },
                    transformScale(film){
                        return Math.round(film.vote_average / 2)
                    }
        
    }
}
</script>

<style lang="scss" scoped>
.fa-solid{
    color: #ffbd00;
}

.product-image {
	transition: all 0.3s ease-out;
	position: relative;
	overflow: hidden;
	display: inline-block;
    margin: 40px;
    box-shadow: rgba(0, 0, 0, 0.3) 0px 19px 38px, rgba(0, 0, 0, 0.22) 0px 15px 12px;
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
    color: #FFF;
    height: 100%;
    width: 100%;
    left: 0;
    top: 0;
}
.info h2 {text-align: center}
.product-image:hover .info{transform: translateX(0);}
.info div{transition: 0.3s ease;}
.product-image:hover img {
    transition: all 0.3s ease-out;
    animation:kenburns-top .5s ease-out both
    }
@keyframes kenburns-top{0%{transform:scale(1) translateY(0);transform-origin:50% 16%}100%{transform:scale(1.25) translateY(-15px);transform-origin:top}}</style>