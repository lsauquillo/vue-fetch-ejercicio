<template>
<div class="postdetail">
 <h3>Post núm.{{id}}</h3> 
 <h2> {{titulo}}</h2>
 <p>{{body}}</p> 
 <button @click="$emit( 'addFavorito', id)" >Favorito</button>
</div>
</template>

<script  setup>
 const props = defineProps ({
  titulo: String,
  body: String,
  id: Number,
  userId: Number,  
 }) 
</script>

<style scoped>
 .postdetail{
  border: 1px solid gray;
  margin: 10px;
  padding: 10px;
 } 
</style>