<template>
  <div id="app">
    <header>
      <app-search/>
    </header>
  </div>
</template>

<script>
import AppSearch from './components/AppSearch.vue'



export default {
  name: 'App',
  components: {
    AppSearch
  }
}
</script>

<style lang="scss">
@import "./assets/style/general.scss";


</style>
