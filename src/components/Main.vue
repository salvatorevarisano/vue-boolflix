<template>
  <main>
      <section>
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
       background:rgba(45, 89, 200, 0.3); //test
       .cards-container {
           display: flex;
           overflow-y: auto;
       }
   }

</style>