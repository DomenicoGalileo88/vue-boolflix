/* Milestone 1:
Creare un layout base con una searchbar (una input e un button) in cui possiamo
scrivere completamente o parzialmente il nome di un film. Possiamo, cliccando il
bottone, cercare sull’API tutti i film che contengono ciò che ha scritto l’utente.
Vogliamo dopo la risposta dell’API visualizzare a schermo i seguenti valori per ogni
film trovato:
1. Titolo
2. Titolo Originale
3. Lingua
4. Voto */

 /* 
 Milestone 2:
Trasformiamo la stringa statica della lingua in una vera e propria bandiera della
nazione corrispondente, gestendo il caso in cui non abbiamo la bandiera della
nazione ritornata dall’API (le flag non ci sono in FontAwesome).
Allarghiamo poi la ricerca anche alle serie tv. Con la stessa azione di ricerca
dovremo prendere sia i film che corrispondono alla query, sia le serie tv, stando
attenti ad avere alla fine dei valori simili (le serie e i film hanno campi nel JSON di
risposta diversi, simili ma non sempre identici)
Qui un esempio di chiamata per le serie tv:
https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it_IT&query=s
crub
  */

<template>
  <div id="app">
    <header>
      <div class="logo"></div>
      <div class="search-film">
        <form action="">
          <label for="">Search Film</label>
          <input class="mx-3" type="text" v-model="titolo" />
          <button @click.prevent="call_API" class="btn btn-danger">
            Search
          </button>
        </form>
      </div>
    </header>

    <main>
      <div class="dati" v-for="movie in movies" :key="movie.id">
        <ul>
          <li>Titolo: {{ movie.title }}</li>
          <li>Titolo originale: {{ movie.original_title }}</li>
          <li v-if="movie.original_language == 'en'">Lingua: <flag iso="gb"/></li>
          <li v-else-if="movie.original_language == 'it'">Lingua: <flag iso="it"/></li>
          <li v-else-if="movie.original_language == 'cn'">Lingua: <flag iso="cn"/></li>
          <li v-else-if="movie.original_language == 'ja'">Lingua: <flag iso="jp"/></li>
          <li v-else-if="movie.original_language == 'es'">Lingua: <flag iso="es"/></li>
          <li v-else-if="movie.original_language == 'fr'">Lingua: <flag iso="fr"/></li>
          <li v-else-if="movie.original_language == 'de'">Lingua: <flag iso="de"/></li>
          <li v-else>Lingua: {{ movie.original_language }}</li>
          <li>Voto: {{ movie.vote_average }}</li>
        </ul>
      </div>
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
      serie_API: "https://api.themoviedb.org/3/search/tv?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it_IT&query="
    };
  },

  methods: {
    call_API() {
      axios
        .get(this.movie_API_initial + this.titolo + this.movie_API_final)
        .then((response) => {
          console.log(response.data.results);
          this.movies = response.data.results;
          this.titolo = '' 
        });

      axios.get(this.serie_API + this.titolo).then((response) =>{
        this.movies += response.data.results
      })
    },
  },

  mounted() {},
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
