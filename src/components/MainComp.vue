<template>
<main>
  <div class="container">
    <h1 class="pb-5">Film</h1>
    <div>
      <CardComp class=" d-flex flex-wrap gap-3" :resultFromApi="resultFromApi"/>
    </div>
  </div>
</main>

  
</template>

<script>
import CardComp from './CardComp.vue';

export default {
    name: "MainComp",
    props: {
        resultFromApi: Array
    },
    components: { CardComp }
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