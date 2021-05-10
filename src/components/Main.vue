<template>
  <main>
      <ul v-for="(movie, i) in searcheredMovie" :key="i">
          <li>{{movie.title}}</li>
          <li>{{movie.original_title}}</li>
          <li>{{movie.original_language}}</li>
          <li>{{movie.vote_average}}</li>
      </ul>
  </main>
</template>

<script>
export default {
    name: 'Main',
    props: ['searcheredMovie'],
    data() {
        return {
            

        }
    },

}
</script>

<style>

</style>