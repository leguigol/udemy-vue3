<script setup>
  import ButtonCounter from './components/ButtonCounter.vue';
  import BlogPost from './components/BlogPost.vue';
  import PaginatePost from './components/PaginatePost.vue'
  import LoadingSpinner from './components/LoadingSpinner.vue'
  
  import { ref } from "vue";

  const posts=ref([]);

  const postXpage=10;
  const inicio=ref(0);
  const fin=ref(postXpage);
  
  const loading=ref(true);

  const next=() => {
    inicio.value=inicio.value+postXpage;
    fin.value= fin.value+postXpage;
  }
  const prev=() => {
    inicio.value=inicio.value-postXpage;
    fin.value= fin.value-postXpage;
  }

  const favorito=ref('')
  const cambiarFavorito = (title) => {
    favorito.value=title
  }

  // fetch('https://jsonplaceholder.typicode.com/posts')
  //   .then(res => res.json())
  //   .then(data => posts.value =data )
  //   .finally(() => {
  //     setTimeout(() => {
  //       loading.value=false
  //     },2000)
  //   });


const fetchData=async () => {
  try {
    const res= await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value=await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(()=> {
      loading.value=false;
    },2000);
  }
}

fetchData()

</script>
<template>
  <LoadingSpinner v-if="loading"/> 
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis Post Favoritos: {{ favorito  }}</h2>

    <!-- <button @click="next">Next Provisorio</button>
    <button @click="prev">Prev Provisorio</button> -->

    <PaginatePost @next="next"
    @prev="prev" :inicio="inicio" :fin="fin" :maxLenght="posts.length"
    class="mb-2"/>    
    <!-- <ButtonCounter />
    <ButtonCounter />
    <ButtonCounter />
    <ButtonCounter /> -->
    <!-- <BlogPost 
      title="Post 1"
      :id="1"
      body="descripcion1"
      colorText="primary"
    />
    <BlogPost 
      title="Post 2"
      :id="2"
      body="descripcion2"
      colorText="secondary"
    />
    <BlogPost 
      title="Post 3"
      :id="3"
      body="descripcion3"
      colorText="success"
    />
    <BlogPost 
      title="Post 4"
      :id="4"
      colorText="primary"
    /> -->

    <BlogPost 
      v-for="post in posts.slice(inicio,fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @cambiarFavoritoNombre="cambiarFavorito"
      class="mb-2"
    ></BlogPost>  

  </div>
</template>

<style></style>