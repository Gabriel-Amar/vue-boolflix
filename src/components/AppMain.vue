<template>
    <div>
        <div class="container-fluid">
            <div class="row">
                <div class="col-2" v-for="pop in popularList" :key="pop.id">
                    <div class="product-image">
                    <img class="img-fluid" :src="image + pop.backdrop_path" alt="">
                    <div class="info">
                        <h5 class="text-center">{{pop.title ? pop.title : pop.name}}</h5>
                            <div>Titolo originale: {{pop.original_title ? pop.original_title : pop.original_name}}</div>
                            <div class="d-flex">Lingua: <country-flag :country='FilmLanguage(pop)' size='normal'/></div>
                            <span v-for="(n,index) in 5" :key="index">
                                <span :class="n <= transformScale(pop) ? 'fa-solid fa-star' : 'fa-regular fa-star'"></span>
                            </span>
                            <div>Trama: {{pop.overview}}</div>
                    </div>
                </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios"
export default {
name: "AppMain",
data(){
    return{
        apiUrl: 'https://api.themoviedb.org/3/',
        apiKey: "f9f88b1e607ce852eb8d91625dc47ba1",
        popularList: [],
        image:'https://image.tmdb.org/t/p/w342'
    }
},
mounted(){
                axios.get(this.apiUrl + "movie/popular" + "?api_key=" + this.apiKey).then((res)=>{
                    this.popularList = res.data.results;
                })
                .catch((err)=>{
                    console.log(err)
                })
            
}
}
</script>

<style lang="scss" scoped>

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
@keyframes kenburns-top{0%{transform:scale(1) translateY(0);transform-origin:50% 16%}100%{transform:scale(1.25) translateY(-15px);transform-origin:top}}
</style>