<template>
<main>

  <div class="container main-container">
    <h1 class="pb-5">Film</h1>
    <div>

      <CardComp v-if="resultFromApi.length > 0" class=" d-flex flex-wrap gap-3" :resultFromApi="resultFromApi"/>
      <div v-else>
        <h2>Nessun risultato</h2>
      </div>
 
    </div>
  </div>

  <div class="container main-container">
    <h1 class="pb-5">Serie Tv</h1>
    <div>
      
      <CardComp v-if="resultFromApi.length > 0" class=" d-flex flex-wrap gap-3" :resultFromApi="resultFromApiSeries"/>
      <div v-else>
        <h2>Nessun risultato</h2>
      </div>

    </div>
  </div>
  


</main>

  
</template>

<script>
import CardComp from './CardComp.vue';


export default {
  name: "MainComp",
  props: {
    resultFromApi: Array,
    resultFromApiSeries: Array
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
.main-container{
  min-height: 00px;
}

</style>