<template>
  <div class="container">
   <div v-for="(result,index) in resultFromApi" :key="`film-${index}`">
    
    <div class=" m-5">
      <h1>Titolo: {{result.title}}</h1>
      <h2>Titolo Originale {{result.original_title}}</h2>
      <h3>Lingua Originale {{result.original_language}}</h3>
      <h4>Media dei voti {{result.vote_average}}</h4>
    </div>
     
   </div>
  </div>
</template>

<script>
export default {
  name: 'MainComp',
  props:{
    resultFromApi: Array
  }
}
</script>

<style>

</style>