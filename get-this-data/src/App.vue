<template>
  <div id="app">
    <!-- Toggle button -->
    <div class="row">
      <div class="col 2 offset-s10">
        <span class="flow-text">
          <div class="switch">
            <label>
              Title 
              <input type="checkbox">
              <span class="lever brown lighten-4"></span>
              Date
            </label>
          </div>
        </span>
      </div>
    </div>

    <!-- Title -->
    <div class="row">
      <div class="col s12 author"><h1>{{ books.data.author }}</h1></div>
    </div>

    <!-- Backround info -->
    <div class="container">
      <div class="row brown lighten-4 author-info">
        <div class="col s6"><h2>Birthday: {{ books.data.birthday }}</h2></div>
        <div class="col s6"><h2>Place of Birth: {{ books.data.birthPlace }}</h2></div>
      </div>
    </div>

    <!-- Books -->
    <div class="row teal lighten-4 books-container">
      <div v-for="item in books.data.books" :key="item.id" class="col s5 book white">
        <div class="col s3 book-thumbnail">
          <img :src="item.imageUrl" alt="image A" />
        </div>
        <div class="col s9 book-content white">
          <ol>
            <li><span class="book-label">Title</span>: {{ item.title }}</li>
            <li>
              <a :href="item.purchaseLink">
                <span class="book-label">Publication Date: {{ item.PublishDate }}</span>
              </a>
            </li> 
          </ol>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data(){
    return{
      books: [],
      errors:[]
    }
  },
  created() {
    axios.get('https://s3.amazonaws.com/api-fun/books.json')
    .then(response => {
      this.books = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
