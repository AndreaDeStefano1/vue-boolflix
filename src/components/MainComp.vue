<template>
<main>

  <div class="container main-container">
    <h1 class="pb-5">Film</h1>

    <div v-if="isLoadedFilms">
      <CardComp v-if="resultFromApi.length > 0" class=" d-flex flex-wrap gap-3" :resultFromApi="resultFromApi"/>
      <div v-else>
        <h2>Nessun risultato</h2>
      </div> 
    </div>
    <div v-else class=" text-center">
      <img src="https://i.gifer.com/ZZ5H.gif" alt="">
    </div>

  </div>

  <div class="container main-container">
    <h1 class="pb-5">Serie Tv</h1>

    <div v-if="isLoadedSeries">      
      <CardComp v-if="resultFromApi.length > 0" class=" d-flex flex-wrap gap-3" :resultFromApi="resultFromApiSeries"/>
      <div v-else>
        <h2>Nessun risultato</h2>
      </div>
    </div>
    <div v-else class=" text-center">
      <img src="https://i.gifer.com/ZZ5H.gif" alt="">
    </div>

  </div>
  


</main>

  
</template>

<script>
import CardComp from './CardComp.vue';


export default {
  name: "MainComp",
  data(){
    return{
     
    }
  },
  props: {
    resultFromApi: Array,
    resultFromApiSeries: Array,
    isLoadedFilms: Boolean,
    isLoadedSeries: Boolean,
  },
  components: { 
    CardComp,
  }
}
</script>

<style lang="scss" scoped>
h1{
  font-size: 80px;
  color: white;
  
}
main{
  background-color: black;
  min-height: 100vh;
}


</style>