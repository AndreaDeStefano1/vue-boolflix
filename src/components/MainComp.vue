<template>
<main>
  <div class="container">
    <h1 class="pb-5">Film</h1>
    <div>
      <CardComp class=" d-flex flex-wrap gap-3" :resultFromApi="resultFromApi"/>
    </div>
  </div>

  <div class="container">
    <h1 class="pb-5">Serie Tv</h1>
    <div>
      <CardCompForSeries class=" d-flex flex-wrap gap-3" :resultFromApiSeries="resultFromApiSeries"/>
    </div>
  </div>
</main>

  
</template>

<script>
import CardComp from './CardComp.vue';
import CardCompForSeries from './CardCompForSeries.vue';

export default {
  name: "MainComp",
  props: {
    resultFromApi: Array,
    resultFromApiSeries: Array
  },
  components: { 
    CardComp,
    CardCompForSeries 
  }
}
</script>

<style lang="scss" scoped>
h1{
  font-size: 100px;
  color: white;
  
}
main{
  background-color: black;
  min-height: 100vh;
}

</style>