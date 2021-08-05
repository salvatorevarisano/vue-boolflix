<template>
  <main>
      <!-- details -->
      <div class="test">
          <section class="details" v-if="details">
              <i class="fas fa-times click-me primary-color" 
              @click="closeDetails()"
              ></i>
                <div>
                    <img :src="backdropImagePathURL + currentMovie.backdrop_path"  :alt="currentMovie.title || currentMovie.name">
                </div>

              <div>
                  <h2 class="primary-color" >{{currentMovie.title || currentMovie.name}}</h2>
                  <div>
                      Release:
                      <span class="primary-color">{{currentMovie.release_date || 'coming soon'}}</span>
                  </div>
                    Description:
                    <p>
                        {{currentMovie.overview || 'Description not available'}}
                    </p>
              </div>
              
          </section>
      </div>
      <section v-show="searcheredMovie.length > 0">
          <h2>Results of research</h2>
          <div class="cards-container">
              <Card  v-for="movie in searcheredMovie" :key="movie.id" :movie="movie" @getDetails ="getDetails"/>
          </div>
      </section>
      <section>
          <h2>Movies</h2>
          <div class="cards-container">
              <Card  v-for="movie in DiscoverMovieList" :key="movie.id" :movie="movie" @getDetails ="getDetails"/>
          </div>
      </section>
      <section>
          <h2>Series</h2>
          <div class="cards-container">
              <Card  v-for="movie in DiscoverTvList" :key="movie.id" :movie="movie" @getDetails ="getDetails"/>
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

    data() {
        return {
            details: false,
            currentMovie: '',
            backdropImagePathURL:'https://image.tmdb.org/t/p/w1280/',
        }
    },

    methods: {
        getDetails(currentMovie) {

            this.currentMovie = currentMovie;
            this.details = true;
            console.log(currentMovie); // test
        },

        closeDetails() {
            this.details = false;
        }
    }

}
</script>

<style lang="scss" scoped>
  @import '@/assets/style/vars.scss';
  @import '@/assets/style/mixins.scss';

    .details {
        display: grid;
        grid-template-columns: 7fr 5fr;
        position: fixed;
        height:calc(100vh - 90px );
        width: 100vw;
        z-index: 9;
        background-color: rgba($bg-color, $alpha: .92);



        .fa-times {
            position: fixed;
            top: 110px;
            right: 10px;
            font-size:3rem;
        }

        & > div {
            justify-self: center;
            align-self: center;

            &:first-of-type {
                text-align: center;
            }
            &:last-of-type {
                flex-direction: column;
                @include flex-center(horizontal);
                height: 100%;
                padding-right: 30px;
                font-size: 1.8rem;
                overflow: auto;
                * {
                    margin-bottom: 10px;
                }
            }

            img {
                object-fit: contain;
                width: 90%;
                height: 90%;
            }
        }
    }
    
    
   section {
       .cards-container {
           display: flex;
           margin-top: 15px;
           margin-bottom: 30px;
           overflow-y: auto;
       }
   }

</style>