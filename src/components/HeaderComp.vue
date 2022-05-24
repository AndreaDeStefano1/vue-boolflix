<template>

<header>
  <nav class=" d-flex justify-content-between p-3">
    <div class="logo">
      <img src="../assets/img/logo.png" alt="">
    </div>
    

    <div class=" d-flex">

      <select v-model="typeToSearch" @change="startSearch(userInput , typeToSearch)" name="searchType" id="">
        <option value="all">All</option>
        <option value="movie">Movie</option>
        <option value="tv">Tv</option>
      </select>

      <input @keyup.enter="startSearch(userInput , typeToSearch)" v-model="userInput" class="" type="text">
      <button  @click="startSearch(userInput , typeToSearch)" class=" btn btn-success">Cerca</button>
    </div>
  </nav>
</header>

</template>

<script>

export default {
  name: 'HeaderComp',
  data(){
    return{
      userInput: '',
      typeToSearch: 'all'
    }
  },
  methods:{
    startSearch(userInput , typeToSearch){
      this.$emit('sendInput', userInput , typeToSearch)
    }
  }

}
</script>

<style lang="scss" scoped>
header{
  width: 100%;
  background-color: #141414;
  img{
    width: 200px;
  }
  input{
    width: 400px;
    margin: 0 10px;

  }
  select{
    width: 100px;
  }
}

</style>