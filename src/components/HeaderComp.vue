<template>

<header>
  <nav class=" d-flex justify-content-between align-items-center p-3">
    <div class="left-side d-flex justify-content-center align-content-center">
      <img src="../assets/img/logo.png" alt="">
      <div class=" ms-3 d-flex align-items-center position-relative">
        <h3 @click="favoritesShow = !favoritesShow" class=" text-light ">Preferiti</h3>
        <div v-if="favoritesShow" class="favorites position-absolute d-flex gap-1 flex-wrap">
          

          
        </div>
      </div>
    </div>
    

    <div class=" d-flex h-100 ">

      <select class="" v-model="typeToSearch" @change="startSearch(userInput , typeToSearch)" name="searchType" id="">
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
  name: "HeaderComp",
  data() {
    return {
      userInput: "",
      typeToSearch: "all",
      favoritesShow: false
    };
  },
  methods: {
    startSearch(userInput, typeToSearch) {
      this.$emit("sendInput", userInput, typeToSearch);
    }
  },
  components: { }
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
    border-radius: 5px;
  }
  select{
    width: 100px;
    border-radius: 5px;
  }
  h3{
    cursor: pointer;
  }
  .favorites{
    min-height: 200px;
    max-height: 500px;
    width: 360px;    
    border: 2px solid red;
    top: 100%;
    z-index: 2;
    border-radius: 10px;
    padding: 20px;
    background-color: #141414;
    overflow-y: scroll;
    &::-webkit-scrollbar {
    display: none;
}
  }
}

</style>