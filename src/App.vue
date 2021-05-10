<template>
  <div id="app">
    <Header @searchKeyword="searchMovies" />
    <Main :searcheredMovie="searcheredMovie"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },

  data() {
    return {
      searcheredMovie: '',
      apiMoviesURL: 'https://api.themoviedb.org/3/search/movie?api_key=990553a5085849ae45ce07713d45c579&query=',
    }
  },

  methods: {
    /**
     * call API and print the results on screan
     */
    searchMovies(userSearch) {
      this.searcheredMovie = userSearch;
      if(this.searcheredMovie !== '') {
        return axios.get(this.apiMoviesURL + this.searcheredMovie)
          .then((res) => {
              this.searcheredMovie = res.data.results;
              console.log(this.searcheredMovie);
          }).catch((error) => {
              console.log(error);
          })
      }
    }
  }
}
</script>

<style lang="scss">


</style>
