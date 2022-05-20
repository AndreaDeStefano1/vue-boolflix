<template>

<header>
  <div class="d-flex p-5">
    <input v-model="userInput" class="form-control" type="text">
    <button @click="$emit('sendInput', userInput)" class=" form-control btn btn-success">Cerca</button>
  </div>
</header>

</template>

<script>

export default {
  name: 'HeaderComp',
  data(){
    return{
      userInput: '',
    }
  }

}
</script>

<style>

</style>