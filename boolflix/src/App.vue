<template>
  <div id="app">
    <SiteHeader v-model="titolo" @search="call_API"/>
    <SiteMain :mixed="mixed" />
    
  </div>
</template>

<script>
import axios from "axios";
import SiteHeader from '@/components/HeaderComponent.vue';
import SiteMain from '@/components/MainComponent.vue';

export default {
  name: "App",
  components: {
    SiteHeader,
    SiteMain
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
      vote: [],
      ok: false,
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
          this.movies = responses[0].data.results;
          this.series = responses[1].data.results;
          this.mixed = this.movies.concat(this.series);
          this.titolo = "";
        })
      );
    },
  },

  mounted() {},
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
