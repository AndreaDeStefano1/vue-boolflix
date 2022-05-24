<template>

  <div>
  
    <div v-for="(result,index) in resultFromApi" :key="`film-${index}`" @mouseenter="show = index" class="film-card" >
  
      <div     
        @mouseleave="show = -1"
        class=" d-flex h-100 position-relative">

        <img v-if="result.poster_path != null" class="h-100 w-100 w-100" :src="`https://image.tmdb.org/t/p/w200${result.poster_path}`" alt="">
        <img v-else src="https://picsum.photos/180/270" alt="">
        <div 
        v-if="show == index" 
        class="film-info position-absolute d-flex flex-column">

          <p> <span>Titolo:</span><br>{{result.title  || result.name}} </p>
          <p> <span>Titolo Originale:</span><br>{{result.original_title || result.original_name}}</p>
          <p><img :src="flagGen(result.original_language)" alt="" class="flag-img"> </p> 
          
          <p>

            <font-awesome-icon 
            icon="fa-solid fa-star" 
            v-for="(starNumber, index) in 5" 
            :key="starNumber"
            :class="{vote : avgVoteToStar(result.vote_average) > index }"
            />

          </p>
          

        </div>

        <div 
        v-if="show == index"
        @mouseleave="showAdd = false" 
        class="film-overview position-absolute">
          <div @click="getCast(result.id), getGenre(result.genre_ids)" class="text position-relative">
             
            <ul v-if="showAdd" class="additional-info position-absolute">
              <span>Attori:</span>
              <li v-for="name in castArray" :key="name">
                {{name}}
              </li>
              <span>Generi:</span>
              <li v-for="genre in genreArray" :key="genre">
                {{genre}}
              </li>
            </ul>
            
            <p v-if="!showAdd">
              Clicca per Maggiori info<br>
              {{result.overview}} 
            </p>
          </div>
          
          
        </div>

      </div>
  
    </div>
  </div>

</template>

<script>
import axios from 'axios';

export default {
  name: 'CardComp',
  props:{
    resultFromApi: Array,
  },
  data(){
    return{
      show: -1,
      flagApiUrl: 'https://countryflagsapi.com/png/',
      linkFlag: '',
      showAdd: false,
      castArray: [],
      genreArray: [],
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
    },
    avgVoteToStar(value){
      value = Math.round(value) / 2
      return value
    },
    getCast(id){
      this.castArray = [];
      axios.get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=09c0eb08b2b03d28fec477a94fe6bd5f&language=it-IT`)
      .then(res => {
        this.showAdd = !this.showAdd
        let castTemporary = res.data.cast
        for (let i = 0; i < 5; i++) {
          const element = castTemporary[i];
          this.castArray.push(element.name)
          
        }
      })
      
    },
    getGenre(genreTemporary){
      this.genreArray = [];
      axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=09c0eb08b2b03d28fec477a94fe6bd5f&language=it-IT`)
      .then(res => {
        let arr = res.data.genres
        genreTemporary.forEach(genre => {
          // console.log(genre )
          for (let i = 0; i < arr.length; i++) {
            const element = arr[i];
            console.log(genre == element.id)
            if(genre == element.id){
              this.genreArray.push(element.name)
            }
            
          }
        console.log('ciao', this.genreArray)
          
        });
      })
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
    border: 1px solid white;
    border-right: none;
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
    .additional-info{
      p{
        font-size: 15px;
      }
      li{
        font-size: 13px;
      }
    }
  }
  .film-info{
    padding: 4px;
    left: 100%;
    height: 100%;
    width: 100%;
    // background-color: #fff8e6;
    background-color: #141414;
    border-top-right-radius: 20px;
    border-bottom-right-radius: 20px;
    border: 1px solid white;
    border-left: none;
    span{
      font-weight: 800;
      color: white;
    }
    p{
      color: white;
      img.flag-img{
        width: 40px;
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
.vote{
  color: rgb(248, 178, 3);
}

</style>