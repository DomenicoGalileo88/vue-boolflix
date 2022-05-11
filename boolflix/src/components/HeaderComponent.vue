<template>
  <header class="d-flex align-items-center justify-content-between p-3">
    <div class="logo">
      <img src="@/assets/img/logo_boolflix.png" alt="logo" />
    </div>
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
  </header>
</template>

<script>
export default {
  name: "SiteHeader",

  props: {
    titolo: String,
  },
};
</script>

<style lang="scss" scoped>
header {
  border-bottom: 1px solid #dc1a2766;
  .btn_boolflix {
    background-color: #dc1a28;
    font-weight: 600;
  }
}
</style>