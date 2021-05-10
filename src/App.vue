<template>
  <div id="app">
    <Header @searchKeyword="searchMovies" />
    <Main :SearchMovie="SearchMovie"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'


export default {
  name: 'App',
  components: {
    Header,
    Main,
  },

  data() {
    return {
      SearchMovie: '',
    }
  },

  methods: {
    searchMovies(userSearch) {
     // console.log('ricerca film', userSearch);
      this.SearchMovie = userSearch;
      //console.log(this.search);
    }
  }
}
</script>

<style lang="scss">


</style>
