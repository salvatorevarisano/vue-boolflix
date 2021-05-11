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
      apiTvURL: 'https://api.themoviedb.org/3/search/tv?api_key=990553a5085849ae45ce07713d45c579&query=',
    }
  },

  methods: {
    /**
     * call API and print the results on screan
     */
    searchMovies(userSearch) {
      this.searcheredMovie = userSearch;
      if(this.searcheredMovie !== '') {
        const requestOne = axios.get(this.apiMoviesURL + this.searcheredMovie);
        const requestTwo = axios.get(this.apiTvURL + this.searcheredMovie);
        axios.all([requestOne, requestTwo]).then(axios.spread((...responses) => {
          const responseOne =  responses[0].data.results
          const responseTwo =  responses[1].data.results
          this.searcheredMovie = responseOne.concat(responseTwo)
          // console.log(responseOne);
          // console.log(responseTwo);
          // console.log(this.searcheredMovie);
        })).catch(errors => {
            console.log(errors);
        })
      }
    }
  }
}
</script>

<style lang="scss">


</style>
