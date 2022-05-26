<template>
  <div class=" position-absolute d-flex gap-1 flex-wrap">
    <div v-for="(film,index) in savedFilms" :key="`savedfilm${index}`" class="saved-card position-relative">
      <img :src="`https://image.tmdb.org/t/p/w200/${film.poster_path}`" alt="">
      <h1 class=" position-absolute">{{film.title || film.name}}</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SavedFilm',
  props :{
    
  }
}
</script>

<style lang="scss" scoped>
.saved-card{
  border: 1px solid white;
  img{
    height: 150px;
  }
}
</style>