<template>
    <div>
        <input v-model="search" @keyup.enter="$emit('performSearch', search)" placeholder="Cerca un film" type="text">
        <button @click="cerca"  type="button" class="btn btn-primary">Cerca Film</button>
    </div>
</template>

<script>


export default {
    name: "AppSearch",
    data(){
        return{
            search:"",
        }
    },
    methods:{
        cerca(){
            this.$emit('performSearch', this.search)
            this.search = ''
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