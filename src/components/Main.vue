<template>
  <main>
      <section>
          <Card  v-for="movie in searcheredMovie" :key="movie.id" :movie="movie"/>
      </section>
      <section>
          <h2>Movies</h2>
          <Card  v-for="movie in DiscoverMovieList" :key="movie.id" :movie="movie"/>
      </section>
      <section>
          <h2>Series</h2>
          <Card  v-for="movie in DiscoverTvList" :key="movie.id" :movie="movie"/>
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
   

</style>