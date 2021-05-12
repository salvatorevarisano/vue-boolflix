<template>
  <main>
      <section>
          <Card  v-for="movie in searcheredMovie" :key="movie.id" :movie="movie"/>
      </section>
  </main>
</template>

<script>
import Card from './Card.vue'

export default {
    name: 'Main',
    props: ['searcheredMovie'],

    components: {
        Card,
    },

}
</script>

<style lang="scss" scoped>
   

</style>