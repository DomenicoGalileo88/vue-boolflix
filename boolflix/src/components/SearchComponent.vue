<template>
  <div class="search-film">
    <!-- il form ascolterà per l'evento submit un evento custom, attraverso l'$emit('search'(è il nome dell'evento))(prevent, serve a prevenire il comportamento di default di ricarica della pagina) -->
    <!-- per far si che tutto funzioni, dobbiamo scrivere il v-model nel seguente modo: :value="titolo" @input="$emit('input', $event.target.value)"  -->
    <form @submit.prevent="$emit('search')">
      <input
        class="mx-3"
        type="search"
        placeholder="Search"
        :value="titolo"
        @input="$emit('input', $event.target.value)"
      />
      <button type="submit" :disabled="titolo < 1" class="btn btn_boolflix">
        Search Film
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  /* passiamo come dato il titolo, che è il risultato del nostro v-model */
  props: {
    titolo: String,
  },
};
</script>

<style lang="scss" scoped>
.btn_boolflix {
  background-color: #dc1a28;
  font-weight: 600;
  border: none;
}
</style>