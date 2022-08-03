<template>
  <header class="d-flex align-items-center justify-content-between p-3">
    <LogoBoolflix />
    <SearchBar v-model="titolo" @search="call_API" />
  </header>
</template>

<script>
import LogoBoolflix from "@/components/LogoComponent.vue";
import SearchBar from "@/components/SearchComponent.vue";
/* importo lo state per salvarci dentro l'array mixed */
import state from "@/state.js";
/* importo axios per fare le chiamate API */
import axios from "axios";

export default {
  name: "SiteHeader",
  components: {
    LogoBoolflix,
    SearchBar,
  },

  data() {
    return {
      movie_API_initial:
        "https://api.themoviedb.org/3/search/movie?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it-IT&query=",
      /* / dati relativi alla prima parte del link dell'api dei film */
      titolo: "",
      /* risultato del v-model dell'imput del searchbar */
      movie_API_final: "&page=1&include_adult=false",
      /* / dati relativi alla seconda parte del link dell'api dei film */
      movies: null,
      /* array che conterrà tutti i film dopo la chiamata axios */
      serie_API:
        "https://api.themoviedb.org/3/search/tv?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it_IT&query=",
      /* prima parte del link api delle serie */
      series: null,
      /* array che conterrà tutte le serie dopo la chiamata axios */ 
    };
  },
  methods: {
    call_API() {
      /* dichiaro una variabile che compone l'intero link dei film  */
      let one = this.movie_API_initial + this.titolo + this.movie_API_final;
      /* dichiaro una variabile che compone l'intero link delle serie  */
      let two = this.serie_API + this.titolo;
      /* console.log(two);
      console.log(one); */

      const request_film = axios.get(one);
      const request_serie = axios.get(two);

      axios.all([request_film, request_serie]).then(
        axios.spread((...responses) => {
        /* richiesta attraverso axios.all (ci permette di fare più chiamate insieme in una) alle API dei film e delle serie */
        /* assegno alla proprietà movies l'array che viene restituito dalla chiamata api dei film */
          this.movies = responses[0].data.results;
        /* assegno alla proprietà series l'array che viene restituito dalla chiamata api delle serie */
          this.series = responses[1].data.results;
          /* assegno alla proprietà mixed dichiarata nello state globale l'array dei film + l'arrey delle serie */
          state.mixed = this.movies.concat(this.series);
          this.titolo = "";
        })
      );
      console.log(state);
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  border-bottom: 1px solid #dc1a2766;
}
</style>