<template>
  <div id="app">
    <SiteHeader />
    <!-- header component -->
    <SiteMain :mixed="mixed" />
    <!-- main component -->
    
  </div>
  <!-- /#app -->
</template>

<script>
/* import components */
import SiteHeader from '@/components/HeaderComponent.vue';
import SiteMain from '@/components/MainComponent.vue';
/* import state.js */
import state from '@/state.js';


export default {
  name: "App",
  components: {
    SiteHeader,
    SiteMain
  },

 computed :{
   /* attraverso questo metodo, ritorniamo con state.mixed i dati relativi all'array mixed dichiarato in header componente */
   mixed(){
     return state.mixed
   }
 }

};
</script>

<style lang="scss">
/* import style */
@import "@/assets/scss/style.scss";
</style>
