<!-- 
Milestone 1:
Creare un layout base con una searchbar (una input e un button) in cui possiamo
scrivere completamente o parzialmente il nome di un film. Possiamo, cliccando il
bottone, cercare sull’API tutti i film che contengono ciò che ha scritto l’utente.
Vogliamo dopo la risposta dell’API visualizzare a schermo i seguenti valori per ogni
film trovato:
1. Titolo
2. Titolo Originale
3. Lingua
4. Voto
 -->

<template>
  <div id="app">
    <header>
      <div class="logo"></div>
      <div class="search-film">
        <form action="">
          <label for="">Search Film</label>
          <input class="mx-3" type="text" v-model="titolo" />
          <button @click.prevent="call_API" class="btn btn-danger">Search</button>
        </form>
      </div>
    </header>

    <main>
      <h1>Titolo:{{titolo}}</h1>
      <div class="dati" v-for="movie in movies" :key="movie.id">
        <h3>Titolo originale:{{movie.original_title}}</h3>
      <h3>lingua:{{movie.original_language}}</h3>
      <h3>Voto:{{movie.vote_average}}</h3>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {
  },

  data() {
    return {
      Url_API_initial: 'https://api.themoviedb.org/3/search/movie?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it-IT&query=',
      titolo: '',
      Url_API_final: '&page=1&include_adult=false',
      movies: null,
    }
  },

  methods: {
    call_API(){
      axios.get(this.Url_API_initial + this.titolo + this.Url_API_final).then((response) =>{
      console.log(response.data.results);
      this.movies = response.data.results
    })
    }
  },

  mounted(){
    
  }
}
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
