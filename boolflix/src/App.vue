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
      <h3>Titolo originale:</h3>
      <h3>lingua:</h3>
      <h3>Voto:</h3>
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
      titolo: '',
      Url_API: `https://api.themoviedb.org/3/search/movie?api_key=feeebc687dcbe2134ac810d7cb75dafe&language=it-IT&query= + titolo + &page=1&include_adult=false`,
    }
  },

  methods: {
    call_API(){
      axios.get(this.Url_API).then((response) =>{
      console.log(response);
      return response
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
