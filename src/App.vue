<template>
  <div id="app">
    <Header @searchKeyword="searchMovies" />
    <Main :searcheredMovie="searcheredMovie" :DiscoverMovieList="DiscoverMovieList"
    :DiscoverTvList="DiscoverTvList"/>
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
      apiURL: 'https://api.themoviedb.org/3/',
      apiKey: '990553a5085849ae45ce07713d45c579',
      movieList: [],
      tvList: [],
      DiscoverMovieList: [],
      DiscoverTvList: [],

    }
  },

  created() {
    // discover
    const requestDiscoverMovie = axios.get(this.apiURL + 'discover/movie', {
      params: {
            api_key: this.apiKey,
      }
    });
    const requestDiscoverTv = axios.get(this.apiURL + 'discover/tv', {
      params: {
            api_key: this.apiKey,
      }
    });
    axios.all([requestDiscoverMovie, requestDiscoverTv]).then(axios.spread((...responses) => {
          this.DiscoverMovieList =  responses[0].data.results
          this.DiscoverTvList =  responses[1].data.results
        })).catch(errors => {
            console.log(errors);
        })
  },

  methods: {
    /**
     * call API and print the results on screan
     */
    searchMovies(userSearch) {
      if(this.userSearch !== '') {
        const requestMovie = axios.get(this.apiURL + 'search/movie', {
          params: {
            api_key: this.apiKey,
            query: userSearch,
          }});
          const requestTv = axios.get(this.apiURL + 'search/tv', {
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

  @import '@/assets/style/general.scss';
  @import '~@fontsource/rubik/300.css';
  @import '~@fontsource/rubik/index.css';
  @import '~@fontsource/rubik/600.css';
  @import '~@fontsource/rubik/700.css';




</style>
