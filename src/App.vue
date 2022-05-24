<template>

  <div>

    <HeaderComp @sendInput='recivedQuery' />
  
    <MainComp
    :resultFromApi="resultFilm"
    :resultFromApiSeries="resultSeries" 
    :isLoadedFilms="isLoadedFilms"
    :isLoadedSeries="isLoadedSeries"
    :showFilms="showFilms"
    :showSeries="showSeries"/>

    

  </div>

</template>

<script>
import HeaderComp from './components/HeaderComp.vue';
import MainComp from './components/MainComp.vue';
import axios from 'axios';


export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp
  },
  data(){
    return{
      queryToPass: '',
      apiUrl: 'https://api.themoviedb.org/3/search/movie',
      apiUrlForSeries: 'https://api.themoviedb.org/3/search/tv',
      resultFilm: [],
      resultSeries: [],
      isLoadedFilms: false,
      isLoadedSeries: false,
      showFilms: false,
      showSeries: false
    }
  },
  methods:{
    recivedQuery(value , value2){
      this.isLoadedFilms = false;
      this.isLoadedSeries = false;
      this.showFilms = false;
      this.showSeries = false;
      this.queryToPass = value;
      if(value2 == 'all'){
        this.getAPI();
        this.getApiForSeries();       
      }
      else if(value2 == 'movie'){
        this.getAPI();
      }
      else if(value2 == 'tv'){
        this.getApiForSeries();
      }
    },
    getAPI(){
      axios.get(this.apiUrl,{
        params: {
          api_key: '09c0eb08b2b03d28fec477a94fe6bd5f',
          language: 'it-IT',
          query: this.queryToPass
        }
      })
      .then(res => {
        console.log(res.data.results , 'sono i res film')
        this.resultFilm = res.data.results;
        this.isLoadedFilms = true;
        this.showFilms = true;
        // serve a ordinare i film dal voto maggiore al voto minore
        this.resultFilm.sort((a, b) =>  b.vote_average - a.vote_average);
      })
    },
    getApiForSeries(){
      axios.get(this.apiUrlForSeries,{
        params: {
          api_key: '09c0eb08b2b03d28fec477a94fe6bd5f',
          language: 'it-IT',
          query: this.queryToPass
        }
      })
      .then(res => {
        console.log(res.data.results , 'sono i res serie')
        this.resultSeries = res.data.results;
        this.isLoadedSeries = true;
        this.showSeries = true;
        // serve a ordinare i film dal voto maggiore al voto minore
        this.resultSeries.sort((a, b) =>  b.vote_average - a.vote_average);
      })
    },
    getTrendingFilm(){
      axios.get('https://api.themoviedb.org/3/trending/movie/week?api_key=09c0eb08b2b03d28fec477a94fe6bd5f')
      .then(res => {
        this.resultFilm = res.data.results;
        this.isLoadedFilms = true;
        this.showFilms = true;
      })
    },
    getTrendingSeries(){
      axios.get('https://api.themoviedb.org/3/trending/tv/week?api_key=09c0eb08b2b03d28fec477a94fe6bd5f')
      .then(res => {
        this.resultSeries = res.data.results;
        this.isLoadedSeries = true;
        this.showSeries = true;
      })
    },

  },
  mounted(){
    this.getTrendingFilm();
    this.getTrendingSeries();
    }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';


</style>
