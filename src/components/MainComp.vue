<template>
<main>
  <div class="container">
    <h1 class="pb-5">Film</h1>
    <div class=" d-flex flex-wrap gap-3">
      <div v-for="(result,index) in resultFromApi" :key="`film-${index}`" @mouseenter="show = index" class="film-card" >
      
        <div     
          @mouseleave="show = -1"
          class=" d-flex h-100 position-relative">

          <img class="h-100 w-100 w-100" :src="`https://image.tmdb.org/t/p/w200${result.poster_path}`" alt="">

          <div 
          v-if="show == index" 
          class="film-info position-absolute d-flex flex-column">

            <p> <span>Titolo:</span><br>{{result.title}} </p>
            <p> <span>Titolo Originale:</span><br>{{result.original_title}}</p>
            <p> <span>Lingua Originale:</span> {{result.original_language}}</p>
            <p> <span>Media dei voti:</span> {{result.vote_average}}</p>

          </div>

          <div 
          v-if="show == index" 
          class="film-overview position-absolute">
            <div class="text">
              <p> {{result.overview}} </p>
            </div>
            
            
          </div>

        </div>
      
      </div>
    </div>
  </div>
</main>

  
</template>

<script>
export default {
  name: 'MainComp',
  props:{
    resultFromApi: Array
  },
  data(){
    return{
      show: -1,
    }
  },
  // computed:{
  //   filteredArray(){
  //     this.resultFromApi.forEach(film => {
  //       if(film.poster_path == null){
  //         this.resultFromApi.remove(film, 1)
  //       }
  //     })
  //       return this.resultFromApi
  //   }
  // }
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
.film-card{
  padding: 10px;
  // background-color: blue;
  // border: 1px solid red;
  width: 200px;  
  transition: all ease 0.5s;
  max-height: fit-content;
  img{
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;
    overflow: hidden;
  }
  .film-overview{
    padding: 10px 3px;
    height: 100%;
    width: 100%;
    overflow: hidden;
    background-color: black;
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;    
    filter: opacity(0.8);
    font-weight: 600;
    top: 50%;
    transform: translateY(-50%);
    .text{
      padding: 5px;
      height: 90%;
      width: 100%;
      overflow: scroll;
      -ms-overflow-style: none;  
      scrollbar-width: none;
      color: white; 
      &::-webkit-scrollbar {
      display: none; 
    }
    }
    
  }
  .film-info{
    padding: 4px;
    left: 100%;
    height: 100%;
    width: 100%;
    background-color: #fff8e6;
     border-top-right-radius: 20px;
    border-bottom-right-radius: 20px;
    span{
      font-weight: 800;
      color: black;
    }
   
  }
  &:hover{
    transform: scale(1.2);
    z-index: 999;
    img,
    .film-info,
    .film-overview{
      margin-left: -50%;
      
    }
    img{
      filter: sepia(0.9);
    }
    
  }


 }
</style>