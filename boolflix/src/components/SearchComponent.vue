<template>
  <div class="search-film">
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
    name: 'SearchBar',

    props: {
        titolo: String,
    },

}
</script>

<style lang="scss" scoped>
.btn_boolflix {
    background-color: #dc1a28;
    font-weight: 600;
    border: none;
  }
</style>