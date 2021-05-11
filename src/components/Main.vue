<template>
  <main>
      <ul v-for="(movie, i) in searcheredMovie" :key="i">
          <li v-if="movie.poster_path !== undefined && movie.poster_path !== null" > <img :src="imagePathURLPartOne + movie.poster_path" :alt="movie.title || movie.name" class="poster"></li>
          <li v-else ><div><img class="poster" src="@/assets/img/censored.png" alt=""></div></li>
          <li>{{movie.title || movie.name}}</li>
          <li>{{movie.original_title || movie.original_name}}</li>
          <li v-if="hasFlag(movie.original_language)"><img class="flag" :src="require(`../assets/img/${movie.original_language}.png`)" :alt="movie.original_language"></li>
          <li v-else >{{movie.original_language}}</li>
          <li v-if="(movie.vote_average > 0)">
              <i class="fas fa-star" v-for="(star, i) in stars(movie.vote_average)" :key="'s' + i"></i>
              <i class="far fa-star" v-for="(emptyStar, i) in ( 5 - stars(movie.vote_average) )" :key="'es' + i"></i>
          </li>
          <li v-else >
              <i class="far fa-star" v-for="(emptyStar, i) in  5" :key="'fes' + i"></i>
          </li>


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
            imagePathURLPartOne: 'https://image.tmdb.org/t/p/w342/',
        }
    },
    methods: {

        hasFlag(language) {
            if(this.flags.includes(language)){
                return true;
            }
        },

        stars(vote) {
            const starsNumber = vote / 2;
            return  Math.round(starsNumber);

        }
    }
}
</script>

<style lang="scss" scoped>
    .flag {
        width: 20px;
    }
    .poster {

        width: 300px;
    }

</style>