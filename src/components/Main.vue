<template>
  <main>
      main content
      {{SearchMovie}}
  </main>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Main',
    props: ['SearchMovie'],
    data() {
        return {
            apiMoviesURL: 'https://api.themoviedb.org/3/search/movie?api_key=990553a5085849ae45ce07713d45c579',
        }
    },
    created() {
        axios.get(this.apiMoviesURL)
            .then((res) => {
                console.log(res.data);
            }).catch((error) => {
                console.log(error);
            })
    }

}
</script>

<style>

</style>