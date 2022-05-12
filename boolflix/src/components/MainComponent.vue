<template>
  <main>
    <div class="container dati_movies">
      <div class="row row-cols-4 pt-4 justify-content-center">
        <div
          class="col text-white text-center p-3 m-3"
          v-for="movie in mixed"
          :key="movie.id"
        >
          <div class="copertina">
            <img
              :src="'https://image.tmdb.org/t/p/w342/' + movie.poster_path"
              alt="copertina"
              v-if="movie.poster_path"
            />
            <img
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS87JUJQ0Y84tjCdxV-DeFa6AGI8DjSznToeg&usqp=CAU"
              alt="copertina"
              v-else
            />
          </div>
          <div class="description p-2">
            <div class="mt-4 title_movie" v-if="movie.title">
              Titolo Film: {{ movie.title }}
            </div>
            <div class="title_serie" v-else>Titolo Serie: {{ movie.name }}</div>

            <div class="original_title_movie" v-if="movie.original_title">
              Titolo originale: {{ movie.original_title }}
            </div>
            <div class="original_name_serie" v-else>
              Titolo originale: {{ movie.original_name }}
            </div>

            <div class="language">
              <div v-if="movie.original_language == 'en'">
                Lingua: <flag iso="gb" />
              </div>
              <div v-else-if="movie.original_language == 'it'">
                Lingua: <flag iso="it" />
              </div>
              <div v-else-if="movie.original_language == 'cn'">
                Lingua: <flag iso="cn" />
              </div>
              <div v-else-if="movie.original_language == 'ja'">
                Lingua: <flag iso="jp" />
              </div>
              <div v-else-if="movie.original_language == 'es'">
                Lingua: <flag iso="es" />
              </div>
              <div v-else-if="movie.original_language == 'fr'">
                Lingua: <flag iso="fr" />
              </div>
              <div v-else-if="movie.original_language == 'de'">
                Lingua: <flag iso="de" />
              </div>
              <div v-else-if="movie.original_language == 'sv'">
                Lingua: <flag iso="sv" />
              </div>
              <div v-else-if="movie.original_language == 'tr'">
                Lingua: <flag iso="tr" />
              </div>

              <div v-else-if="movie.original_language == 'pt'">
                Lingua: <flag iso="pt" />
              </div>

              <div v-else-if="movie.original_language == 'pl'">
                Lingua: <flag iso="pl" />
              </div>

              <div v-else>Lingua: {{ movie.original_language }}</div>
            </div>
            <!-- /.language -->

            <div class="star">
              <span>Voto: </span>
              <span
                v-for="(star, i) in Math.round(
                  Math.round(movie.vote_average) / 2
                )"
                :key="i"
                ><font-awesome-icon icon="fa-solid fa-star" class="gold"
              /></span>
              <span
                v-for="(star, i) in 5 -
                Math.round(Math.round(movie.vote_average) / 2)"
                :key="i + 10"
                ><font-awesome-icon icon="fa-solid fa-star" class="grey"
              /></span>
            </div>
            <!-- /.star -->

            <div v-if="movie.overview" class="overview p-2">
              Overview: {{ movie.overview }}
            </div>
          </div>
        </div>
        <!-- /.col -->
      </div>
      <!-- /.row -->
    </div>
    <!-- /.dati_movies -->
  </main>
</template>

<script>
/* import state from '@/state.js'; */
/* export component */
export default {
  name: "SiteMain",
/* Passo attraverso la props l'array mixed che contiene le serie tv e i film selezionati attraverso la search bar. (L'array mixed si trova fisicamente in header component, perchè è li che vengono fatte le chiamate Api con axios, ma noi ci rivolgiamo ad app.vue componente, perchè è li che importiamo lo state, dove dentro abbiamo salvato i dati dell'array mixed) */
  props: 
      ['mixed'],

      /* oppure lo possiamo fare con lo state */

 /*  computed :{
   mixed(){
     return state.mixed
   }
 } */
     /* attraverso questo metodo, ritorniamo con state.mixed i dati relativi all'array mixed dichiarato in header componente */
  
};


</script>

<style lang="scss" scoped>
main {
  div {
    font-size: 0.8rem;
  }
  .col {
    box-shadow: 0px 0px 12px 3px #dc1a28;
    position: relative;
    cursor: pointer;
    &:hover .description {
      display: block;
    }

    .description {
      display: none;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(21, 0, 0, 0.8);

      .overview {
        font-size: 0.6rem;
      }
    }

    img {
      width: 290px;
      height: 420px;
    }
    .gold {
      color: goldenrod;
    }

    .grey {
      color: lightgrey;
    }
  }
}
</style>