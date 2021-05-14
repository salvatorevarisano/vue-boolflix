<template>
  <main>
      <section v-show="searcheredMovie.length > 0">
          <h2>Results of research</h2>
          <div class="cards-container">
              <Card  v-for="movie in searcheredMovie" :key="movie.id" :movie="movie"/>
          </div>
      </section>
      <section>
          <h2>Movies</h2>
          <div class="cards-container">
              <Card  v-for="movie in DiscoverMovieList" :key="movie.id" :movie="movie"/>
          </div>
      </section>
      <section>
          <h2>Series</h2>
          <div class="cards-container">
              <Card  v-for="movie in DiscoverTvList" :key="movie.id" :movie="movie"/>
          </div>
      </section>
  </main>
</template>

<script>
import Card from './Card.vue'

export default {
    name: 'Main',
    props: ['searcheredMovie', 'DiscoverMovieList', 'DiscoverTvList', ],

    components: {
        Card,
    },

}
</script>

<style lang="scss" scoped>
   section {
       .cards-container {
           display: flex;
           margin-top: 15px;
           margin-bottom: 30px;
           overflow-y: auto;
       }
   }

</style>