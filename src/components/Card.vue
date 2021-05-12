<template>
  <div class="card">
        <!-- movie poster -->
        <img class="poster" v-if="movie.poster_path !== undefined && movie.poster_path !== null" 
            :src="imagePathURLPartOne + movie.poster_path"
            :alt="movie.title || movie.name" 
        >
        <img v-else class="poster" src="@/assets/img/censored.png" :alt="movie.title || movie.name">

        <!-- movie info -->
        <div class="overlay">
            <h2>{{movie.title || movie.name}}</h2>
            <div v-show="(movie.title || movie.name) !== (movie.original_title || movie.original_name)">
                <span>original title</span>
                <h3>{{movie.original_title || movie.original_name}}</h3>
            </div>
            <div v-if="hasFlag(movie.original_language)">
                <img class="flag" :src="require(`../assets/img/${movie.original_language}.png`)" :alt="movie.original_language">
            </div>
            <div v-else >
                {{movie.original_language}}
            </div>
            <span v-if="(movie.vote_average > 0)">
                <i class="fas fa-star" v-for="(star, i) in stars(movie.vote_average)" :key="'s' + i"></i>
                <i class="far fa-star" v-for="(emptyStar, i) in ( 5 - stars(movie.vote_average) )" :key="'es' + i"></i>
            </span>
            <span v-else >
                <i class="far fa-star" v-for="(emptyStar, i) in  5" :key="'fes' + i"></i>
            </span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['movie'],

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