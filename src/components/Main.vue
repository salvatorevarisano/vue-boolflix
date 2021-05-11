<template>
  <main>
      <ul v-for="(movie, i) in searcheredMovie" :key="i">
          <li>{{movie.title || movie.name}}</li>
          <li>{{movie.original_title || movie.original_name}}</li>
          <!-- <li>{{printFlag(movie.original_language)}}</li>  -->
          <li v-if="hasFlag(movie.original_language)"><img class="flag" :src="require(`../assets/img/${movie.original_language}.png`)" :alt="movie.original_language"></li>
          <li v-else >{{movie.original_language}}</li>
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
            flags: ['it', 'en'],
        }
    },
    methods: {
        // img non viene interpretato come tag ma come stringa
        //  printFlag(language) {
        //      if(this.flags.includes(language)) {
        //          return `<img :src="require(../assets/img/${language}.png)" alt="${language}">`;
        //      }
        //      return language
        //  }

        hasFlag(language) {
            if(this.flags.includes(language)){
                return true;
            }
        },
    }
}
</script>

<style lang="scss" scoped>
    .flag {
        width: 20px;
    }

</style>