 /*Milestone 3:
In questa milestone come prima cosa aggiungiamo la copertina del film o della serie
al nostro elenco. Ci viene passata dall’API solo la parte finale dell’URL, questo
perché poi potremo generare da quella porzione di URL tante dimensioni diverse.
Dovremo prendere quindi l’URL base delle immagini di TMDB:
https://image.tmdb.org/t/p/ per poi aggiungere la dimensione che vogliamo generare
(troviamo tutte le dimensioni possibili a questo link:
https://www.themoviedb.org/talk/53c11d4ec3a3684cf4006400) per poi aggiungere la
parte finale dell’URL passata dall’API.
Esempio di URL:
https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png
Trasformiamo poi il voto da 1 a 10 decimale in un numero intero da 1 a 5, così da
permetterci di stampare a schermo un numero di stelle piene che vanno da 1 a 5,
lasciando le restanti vuote (troviamo le icone in FontAwesome).
Arrotondiamo sempre per eccesso all’unità successiva, non gestiamo icone mezze
piene (o mezze vuote :P)*/
  
  <script>
export default {};
</script>
  
  <style>
</style> */



<template>
  <div id="app">
    <header>
      <div class="logo">
        <img src="@/assets/img/logo_boolflix.png" alt="logo" />
      </div>
      <div class="search-film">
        <form action="">
          <label for="">Search Film</label>
          <input class="mx-3" type="text" v-model="titolo" />
          <button @click.prevent="call_API" class="btn btn-danger">
            Search Film
          </button>

          <!-- <button @click.prevent="call_API_series" class="btn btn-danger ms-3">
            Search Serie
          </button> -->
        </form>
      </div>
    </header>

    <main>
      <div class="dati_movies" v-for="(movie, index) in mixed" :key="movie.id">
        <ul>
          <li>
            <img
              :src="'https://image.tmdb.org/t/p/w200/' + movie.poster_path"
              alt="copertina"
            />
          </li>
          <li v-if="movie.title">Titolo Film: {{ movie.title }}</li>
          <li v-else>Titolo Serie: {{ movie.name }}</li>

          <li v-if="movie.original_title">
            Titolo originale: {{ movie.original_title }}
          </li>
          <li v-else>Titolo originale: {{ movie.original_name }}</li>

          <li v-if="movie.original_language == 'en'">
            Lingua: <flag iso="gb" />
          </li>
          <li v-else-if="movie.original_language == 'it'">
            Lingua: <flag iso="it" />
          </li>
          <li v-else-if="movie.original_language == 'cn'">
            Lingua: <flag iso="cn" />
          </li>
          <li v-else-if="movie.original_language == 'ja'">
            Lingua: <flag iso="jp" />
          </li>
          <li v-else-if="movie.original_language == 'es'">
            Lingua: <flag iso="es" />
          </li>
          <li v-else-if="movie.original_language == 'fr'">
            Lingua: <flag iso="fr" />
          </li>
          <li v-else-if="movie.original_language == 'de'">
            Lingua: <flag iso="de" />
          </li>
          <li v-else-if="movie.original_language == 'sv'">
            Lingua: <flag iso="sv" />
          </li>
          <li v-else-if="movie.original_language == 'tr'">
            Lingua: <flag iso="tr" />
          </li>

          <li v-else-if="movie.original_language == 'pt'">
            Lingua: <flag iso="pt" />
          </li>
          <li v-else>Lingua: {{ movie.original_language }}</li>

          <li v-for="(star, i) in vote[index] " :key="i"><font-awesome-icon icon="fa-solid fa-star" /></li>
        </ul>
      </div>

      <!-- <div class="dati_series" v-for="serie in series" :key="serie.id">
        <ul>
          <li>Titolo Serie: {{ serie.name }}</li>

          <li>Titolo originale: {{ serie.original_name }}</li>
          <li v-if="serie.original_language == 'en'">
            Lingua: <flag iso="gb" />
          </li>
          <li v-else-if="serie.original_language == 'it'">
            Lingua: <flag iso="it" />
          </li>
          <li v-else-if="serie.original_language == 'cn'">
            Lingua: <flag iso="cn" />
          </li>
          <li v-else-if="serie.original_language == 'ja'">
            Lingua: <flag iso="jp" />
          </li>
          <li v-else-if="serie.original_language == 'es'">
            Lingua: <flag iso="es" />
          </li>
          <li v-else-if="serie.original_language == 'fr'">
            Lingua: <flag iso="fr" />
          </li>
          <li v-else-if="serie.original_language == 'de'">
            Lingua: <flag iso="de" />
          </li>
          <li v-else>Lingua: {{ serie.original_language }}</li>
          <li>Voto: {{ serie.vote_average }}</li>
        </ul>
      </div> -->
    </main>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},

  data() {
    return {
      movie_API_initial:
        "https://api.themoviedb.org/3/search/movie?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it-IT&query=",
      titolo: "",
      movie_API_final: "&page=1&include_adult=false",
      movies: null,
      series: null,
      serie_API:
        "https://api.themoviedb.org/3/search/tv?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it_IT&query=",
      mixed: null,
      vote: [],
    };
  },

  methods: {
    call_API() {
      let one = this.movie_API_initial + this.titolo + this.movie_API_final;
      let two = this.serie_API + this.titolo;

      const request_film = axios.get(one);
      const request_serie = axios.get(two);

      axios.all([request_film, request_serie]).then(
        axios.spread((...responses) => {
          //console.log(response.data.results);
          this.movies = responses[0].data.results;
          this.series = responses[1].data.results;
          this.mixed = this.movies.concat(this.series);
          this.titolo = "";
        })
      );
    },

    /* call_API_series() {
      axios
      .get(this.serie_API + this.titolo)
      .then((response) => {
        console.log(response.data.results);
        this.series = response.data.results;
      });
    }, */
  },

  mounted() {},

  computed: {
    starVote() {
      this.mixed.forEach((element) => {
        let vote = element.vote_average;
        //return console.log(Math.floor(vote));
        let star_vote = Math.round(Math.round(vote) / 2);
        //return console.log(star_vote);
        return this.vote.push(star_vote);
        //return console.log(this.vote);
      });
    },

   /*  generateStar() {
      let starNumber = this.vote[i];
      for(let i = 0; i < this.vote[i]; i++){
        let star = `<font-awesome-icon icon="fa-duotone fa-star" />`;
        return console.log(star);
        
      }
    }, */
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
