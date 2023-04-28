<template>
  <LoadingSpinner v-if="loading"/>
  <div class="postlist" v-else>
    <h3>Favorito {{ favorito }}</h3>
    <PostPagination
      @prev="handlePrev"
      @next="handleNext"
      :inicio="inicio"
      :final="final"
      :maxlength="posts.length"
    />
    <div class="post-detail">
      <PostDetail
        v-for="post in posts.slice(inicio, final)"
        :id="post.id"
        :titulo="post.title"
        :key="post.id"
        :body="post.body"        
        @addFavorito="handleFavorito"
      />
    </div>
  </div>
</template>

<script  setup>
import { ref, onMounted } from "vue";
import PostDetail from "../components/PostDetail.vue";
import PostPagination from "../components/PostPagination.vue";
import LoadingSpinner from "../components/LoadingSpinner.vue"

const loading = ref(true)
const posts = ref([]);
const inicio = ref(0);
const postperpage = 10;
const final = ref(inicio.value + postperpage);


/* Utilizando promesas .then .catch .finally

fetch("https://jsonplaceholder.typicode.com/posts")
  .then((res) => res.json())
  .then((data) => (posts.value = data))
  .catch( error => {
    console.log( error)
  })
  .finally(()=>{
    setTimeout(()=>{
      loading.value = false
    }, 2000)
  })

*/

/* Utilizando async await */

const fetchdata = async()=>{
  try{
     const res = await fetch("https://jsonplaceholder.typicode.com/posts")
 posts.value = await res.json() 
  }
  catch(err){
    console.log(err)
  }
  finally{
     setTimeout(()=>{
      loading.value = false
    }, 2000)
  } 
}
fetchdata();



/*Utilizando omMounted 

onMounted(() => {
  fetch("https://jsonplaceholder.typicode.com/posts")
  .then((res) => res.json())
  .then((data) => (posts.value = data))
  .catch( error => {
    console.log( error)
  })
  .finally(()=>{
    setTimeout(()=>{
      loading.value = false
    }, 2000)
  })
})

*/

const favorito = ref("");
const handleFavorito = (num) => {
  favorito.value = num;
  console.log(num);
};

const handleNext = () => {
  inicio.value = inicio.value + postperpage;
  final.value = final.value + postperpage;
  console.log(posts.value.length);
};
const handlePrev = () => {
  inicio.value = inicio.value - postperpage;
  final.value = final.value - postperpage;
  console.log(inicio.value, final.value);
};
</script>

<style scoped>
.postlist {
  border: 1px solid black;
  padding: 10px;
}
</style>