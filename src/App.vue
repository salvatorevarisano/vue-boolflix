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
      apiURL: 'https://api.themoviedb.org/3/search/',
      apiKey: '990553a5085849ae45ce07713d45c579',
      movieList: [],
      tvList: [],
    }
  },

  methods: {
    /**
     * call API and print the results on screan
     */
    searchMovies(userSearch) {
      if(this.userSearch !== '') {
        const requestMovie = axios.get(this.apiURL + 'movie', {
          params: {
            api_key: this.apiKey,
            query: userSearch,
          }});
          const requestTv = axios.get(this.apiURL + 'tv', {
          params: {
            api_key: this.apiKey,
            query: userSearch,
          }});
        axios.all([requestMovie, requestTv]).then(axios.spread((...responses) => {
          this.movieList =  responses[0].data.results
          this.tvList =  responses[1].data.results
          this.searcheredMovie = this.movieList.concat(this.tvList)
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
