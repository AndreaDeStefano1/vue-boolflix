<template>

  <div>
  
    <div v-for="(result,index) in resultFromApiSeries" :key="`film-${index}`" @mouseenter="show = index" class="film-card" >
  
      <div     
        @mouseleave="show = -1"
        class=" d-flex h-100 position-relative">

        <img class="h-100 w-100 w-100" :src="`https://image.tmdb.org/t/p/w200${result.poster_path}`" alt="">

        <div 
        v-if="show == index" 
        class="film-info position-absolute d-flex flex-column">

          <p> <span>Titolo:</span><br>{{result.name}} </p>
          <p> <span>Titolo Originale:</span><br>{{result.original_name}}</p>
          <p><img :src="flagGen(result.original_language)" alt="" class="flag-img"> </p> 
          <p> <span>Media dei voti:</span> {{result.vote_average}}</p>

        </div>

        <!-- <div 
        v-if="show == index" 
        class="film-overview position-absolute">
          <div class="text">
            <p> {{result.overview}} </p>
          </div>
          
          
        </div> -->

      </div>
  
    </div>
  </div>

</template>

<script>
//import axios from 'axios';

export default {
  name: 'CardCompForSeries',
  props:{
    resultFromApiSeries: Array,
  },
  data(){
    return{
      show: -1,
      flagApiUrl: 'https://countryflagsapi.com/png/',
      linkFlag: ''
    }
  },
  methods:{
    fixFlag(value){
      //qui inserisco le sigle delle bandiere la cui sigla non corrisponde a quella che mi arriva dall' api
      if(value == 'en') return 'gb'
      if(value == 'ja') return 'jp'
      else return value
    },
    flagGen(value){
      value = this.fixFlag(value)
      return 'https://countryflagsapi.com/png/' + value
    }
  }

}
</script>

<style lang="scss" scoped>

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
    p{
      img.flag-img{
        width: 30px;
        filter: none;
        border-top-left-radius: 0;
        border-bottom-left-radius: 0;
        margin-left: 0;
      }
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