<template>
  <div class="card">
        <!-- movie poster -->
        <img class="poster" v-if="movie.poster_path !== undefined && movie.poster_path !== null" 
            :src="imagePathURLPartOne + movie.poster_path"
            :alt="movie.title || movie.name" 
        >
        <img v-else class="poster" src="@/assets/img/poster-placeholder.png" :alt="movie.title || movie.name">

        <!-- movie info -->
            <div class="overlay">
                <div>
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
                    <div class="click-me cta" @click="$emit('getDetails', currentMovie)" >details</div>
                </div>
            </div>
        </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['movie'],

    data() {
        return {
            flags: ['it', 'en', 'fr', 'de', 'es'],
            imagePathURLPartOne: 'https://image.tmdb.org/t/p/w342/',
            currentMovie: this.movie,
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

    @import '@/assets/style/vars.scss';
    @import '@/assets/style/mixins.scss';

    .card {
        position:relative;
        flex-shrink: 0;
        width: 300px;
        margin: 5px;
        overflow-y: hidden;
        &:hover .overlay {
            bottom: 0;
        }
         .poster {
            display: block;
            width: 100%;
            height: 100%;
            object-fit: cover;
         }
        .overlay {
            @include flex-center();
            position: absolute;
            bottom: -60%;
            left: 0;
            width: 100%;
            height: 60%;
            padding: 10px;
            text-align: center;
            background-color: rgba($primary-color, 0.9);
            color: $text-color;
            overflow-y: auto;
            border-radius: 15px 15px 0 0;
            transition: 0.8s;

            & > div {
                width: 100%;
                & > * {
                    margin-bottom: 10px;
                }
            }
            h2 {
                font-size: 1.3rem;
            };
            h3 {
                font-size: 1rem;
            }
            .cta {
                width: 40%;
                margin: 20px auto;
                padding:10px;
                border: 1px solid currentColor;
                border-radius:15px;
            }
           
        }
    }
     .flag {
        width: 20px;
    }
</style>