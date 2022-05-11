<template>
  <header class="d-flex align-items-center justify-content-between p-3">
    <LogoBoolflix />
    <SearchBar v-model="titolo" @search="call_API" />
  </header>
</template>

<script>
import LogoBoolflix from "@/components/LogoComponent.vue";
import SearchBar from "@/components/SearchComponent.vue";
import state from "@/state.js";
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
      titolo: "",
      movie_API_final: "&page=1&include_adult=false",
      movies: null,
      series: null,
      serie_API:
        "https://api.themoviedb.org/3/search/tv?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it_IT&query=",
      mixed: null,
    };
  },
  methods: {
    call_API() {
      let one = this.movie_API_initial + this.titolo + this.movie_API_final;
      let two = this.serie_API + this.titolo;
      console.log(two);
      console.log(one);

      const request_film = axios.get(one);
      const request_serie = axios.get(two);

      axios.all([request_film, request_serie]).then(
        axios.spread((...responses) => {
          this.movies = responses[0].data.results;
          this.series = responses[1].data.results;
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