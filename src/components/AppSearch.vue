<template>
    <div>
        
            <div class="container-fluid">
                <div class="align">
                <a href=""  class="navbar-brand navbar-dark bg-dark fw-bold display-2">Boolflix</a>
                  <div class="home" href="" value="refresh" onclick="history.go(0)">Home</div>
                </div>
                <div class="search-box">
                    <button @click="$emit('performSearch', search)" class="btn-search"><i class="fas fa-search"></i></button>
                    <input class="input-search" v-model="search" @keyup.enter="$emit('performSearch', search)" placeholder="Cerca un film o una serie" type="text">
                </div>
                
                  
                </div>
                
            
        
        
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
        },
    },
    computed:{
        
    }
}
</script>

<style lang="scss">
@import "../assets/style/general.scss";
.container-fluid{
display: flex;
  margin: 10px;
      justify-content: space-between;
    align-items: center;
}
.navbar-brand{
    color: $red !important;
    font-size: 25px !important;
}
.align{
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.home{
    padding-top: 4px;
    font-weight: bold;
    color: whitesmoke;
}
.home:hover{
  text-decoration: underline;
  cursor: pointer;
}

.search-box{
  width: fit-content;
  height: fit-content;
  position: relative;
}
.input-search{
  height: 50px;
  width: 50px;
  border-style: none;
  padding: 10px;
  font-size: 18px;
  letter-spacing: 2px;
  outline: none;
  border-radius: 25px;
  transition: all .5s ease-in-out;
  background-color: #212529;
  padding-right: 40px;
  color:#fff;
}
.input-search::placeholder{
  color:rgba(255,255,255,.5);
  font-size: 18px;
  letter-spacing: 2px;
  font-weight: 100;
}
.btn-search{
  width: 50px;
  height: 50px;
  border-style: none;
  font-size: 20px;
  font-weight: bold;
  outline: none;
  cursor: pointer;
  border-radius: 50%;
  position: absolute;
  right: 0px;
  color:#ffffff ;
  background-color:transparent;
  pointer-events: painted;  
}
.btn-search:focus ~ .input-search{
  width: 300px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom:1px solid rgba(255,255,255,.5);
  transition: all 500ms cubic-bezier(0, 0.110, 0.35, 2);
}
.input-search:focus{
  width: 300px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom:1px solid rgba(255,255,255,.5);
  transition: all 500ms cubic-bezier(0, 0.110, 0.35, 2);
}

</style>