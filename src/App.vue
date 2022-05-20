<template>

  <div>

    <HeaderComp @sendInput='recivedQuery'
    />

    <MainComp
    :resultFromApi="result"/>

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
      queryToPass: 'potter',
      apiUrl: 'https://api.themoviedb.org/3/search/movie',
      result: []
    }
  },
  methods:{
    recivedQuery(value){
      this.queryToPass = value;
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
        console.log(res.data.results , 'sono i res')
        this.result = res.data.results;
        
      })
    },
  },
  mounted(){
    this.getAPI()
  }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';


</style>
