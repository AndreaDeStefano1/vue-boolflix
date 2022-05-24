<template>

<header>
  <nav class=" d-flex justify-content-between p-3">
    <div class="logo">
      <img src="../assets/img/logo.png" alt="">
    </div>
    <select v-model="typeToSearch" name="" id="">
      <option value="all">All</option>
      <option value="movie">Movie</option>
      <option value="tv">Tv</option>
    </select>
    <div class=" d-flex">
      <input @keyup.enter="startSearch(userInput)" v-model="userInput" class="" type="text">
      <button  @click="startSearch(userInput)" class=" btn btn-success">Cerca</button>
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
    startSearch(value){
      this.$emit('sendInput', value)
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
}

</style>