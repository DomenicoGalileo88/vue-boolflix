<template>
  <div id="app">
    <SiteHeader />
    <SiteMain :mixed="mixed" />
    
  </div>
</template>

<script>

import SiteHeader from '@/components/HeaderComponent.vue';
import SiteMain from '@/components/MainComponent.vue';
import state from '@/state.js';


export default {
  name: "App",
  components: {
    SiteHeader,
    SiteMain
  },

 computed :{
   mixed(){
     return state.mixed
   }
 }

};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
