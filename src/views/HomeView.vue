<template>
 <div>
 <div class="container">
 <form @submit.prevent="searchBook" >
 <div class="columns">
 <div class="column is-8 is-offset-2">
 <div class="field has-text-centered mt-5">
  
  <div class="control">
    <input class="input has-text-centered" type="text" placeholder="Kitob qidirish uchun so'z kiriting 🔎" v-model="key">
  
  </div>
</div>

 </div>
  <div class="column is-2 ">
 <div class="field has-text-centered mt-5">
  
  <div class="control">
   <button class="button is-primary" >Qidirish</button>
  </div>
</div>

 </div>

 </div></form>
 </div>

<!-- Searched books -->
<div class="container mt-3" v-if="searchbooks.length">
<h1 class="has-text-centered title" style="color:green">Qidirilgan kitoblar</h1>
<div class="columns is-multiline ">


<div class="column is-4 " v-for="book in searchbooks" :key="book.id">
<div class="card">
  <div class="card-image">
    <figure class="image is-4by3">
      <img :src="book.image"    alt="Kitob rasmi">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
        <figure class="image is-48x48">
          <img :src="book.image" alt="Kitob rasmi">
        </figure>
      </div>
      <div class="media-content">
        <p class="title is-4">{{book.name}}</p>
        <p class="subtitle is-6">{{book.author}}</p>
      </div>
    </div>

    <div class="content">
    <p> {{book.description}}</p>
    <p>Kitob janrlari</p>
      <br>
      <time datetime="2016-1-1" >{{formatDate(book.uploaded_at)}}</time>
    </div>
  </div>


 <footer class="card-footer">
    <a :href="book.file" class="card-footer-item" @click="adddownloadcounter(book.url)"  target="_blank" download ><i class="fa fa-download" ></i>{{book.downloaded}}</a>
    <a href="#" class="card-footer-item"><i class="fa fa-eye" ></i> {{book.viewed}}</a>
    <a href="#" class="card-footer-item"><i class="fas fa-share"></i>{{book.shared}}</a>
  </footer></div>
</div>




</div>

</div>
<!-- Ended Searched books -->
 <!-- Search -->

<div class="container mt-3">
<h1 class="has-text-centered title" style="color:green">Ko'p yuklangan kitoblar</h1>
<div class="columns is-multiline ">


<div class="column is-4 " v-for="book in books" :key="book.id">
<div class="card">
  <div class="card-image">
    <figure class="image is-4by3">
      <img :src="book.image"    alt="Kitob rasmi">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
        <figure class="image is-48x48">
          <img :src="book.image" alt="Kitob rasmi">
        </figure>
      </div>
      <div class="media-content">
        <p class="title is-4">{{book.name}}</p>
        <p class="subtitle is-6">{{book.author}}</p>
      </div>
    </div>

    <div class="content">
    <p> {{book.description}}</p>
    <p>Kitob janrlari</p>
      <br>
      <time datetime="2016-1-1" >{{formatDate(book.uploaded_at)}}</time>
    </div>
  </div>


 <footer class="card-footer">
    <a :href="book.file" class="card-footer-item" @click="adddownloadcounter(book.url)"  target="_blank" download ><i class="fa fa-download" ></i>{{book.downloaded}}</a>
    <a href="#" class="card-footer-item"><i class="fa fa-eye" ></i> {{book.viewed}}</a>
    <a href="#" class="card-footer-item"><i class="fas fa-share"></i>{{book.shared}}</a>
  </footer></div>
</div>




</div>
</div>
<!-- Pagination -->


<!-- Favorite -->



 </div>
</template>
<style scoped>
input{
  border-radius: 15px;
  height: 50px;
}
button{
  border-radius: 15px;
  height: 50px;
}
</style>
<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'
import moment from 'moment'
export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  data(){
    return {
      books:[],
      key:'',
      searchbooks:[],
       url:'https://bigbookuz.pythonanywhere.com/api/v1',
    }
  },
  
  methods:{
    searchBook(){
         
          axios.get(`/search/${this.key}/`).then((res) => 
              this.searchbooks = res.data
            )
     
    },

      formatDate(date) {
        return moment(date).format('DD-MM-YYYY');
    },
    adddownloadcounter(url){
            axios.get(`${url}download/`).then(
              this.getmorebooks() 
            )
            
             
    },
    getmorebooks(){

      const data = axios.get('/more').then((res) => 
      this.books = res.data
      )
     
    }
  },
  mounted(){
    this.getmorebooks();
  }
}
</script>
