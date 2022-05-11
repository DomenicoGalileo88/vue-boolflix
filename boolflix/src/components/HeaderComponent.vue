<template>
  <header class="d-flex align-items-center justify-content-between p-3">
    <LogoBoolflix />
    <SearchBar v-model="titolo" titolo="titolo"/>
  </header>
</template>

<script>
import LogoBoolflix from '@/components/LogoComponent.vue';
import SearchBar from '@/components/SearchComponent.vue';

export default {
  name: "SiteHeader",
    components:{
        LogoBoolflix,
        SearchBar,
    },

  props: {
    titolo: String,
  },

};
</script>

<style lang="scss" scoped>
header {
  border-bottom: 1px solid #dc1a2766;
}
</style>