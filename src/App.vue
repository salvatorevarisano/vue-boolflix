<template>
  <div id="app">
    <Header @searchKeyword="searchMovies" />
    <Main :SearchMovie="SearchMovie"/>
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
      SearchMovie: '',
      apiMoviesURL: 'https://api.themoviedb.org/3/search/movie?api_key=990553a5085849ae45ce07713d45c579&query=',
    }
  },

  methods: {
    searchMovies(userSearch) {
     // console.log('ricerca film', userSearch);
      this.SearchMovie = userSearch;
      if(this.SearchMovie !== '') {
                 return axios.get(this.apiMoviesURL + this.SearchMovie)
                    .then((res) => {
                        // this.test = res.data;
                        this.SearchMovie = res.data;
                        console.log(res.data);
                    }).catch((error) => {
                        console.log(error);
                    })
            }
      //console.log(this.search);
    }
  }
}
</script>

<style lang="scss">


</style>
