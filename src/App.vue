<script>
import axios from 'axios';
import { apiUri, apiKey } from './data'
export default {
  name: 'Boolflix',
  data() {
    return {
      searchWord: '',
      moviesList: []
    }
  },
  methods: {
    // get movies by name from the API
    fetchMovies() {
      if (!this.searchWord) return
      axios.get(`${apiUri}/search/movie?api_key=${apiKey}&query=${this.searchWord}`)
        .then(res => {
          this.moviesList = res.data.results;
        })
        .catch(err => { console.error(err) })

    }
  }
}
</script>

<template>
  <!-- # Search Bar -->
  <form @submit.prevent="fetchMovies">
    <input type="text" placeholder="Cerca..." v-model.trim="searchWord">
    <button>Cerca</button>
  </form>

  <!-- # Movies list -->
  <ul>
    <li v-for="movie in moviesList" :key="movie.id">{{ movie.title }}</li>
  </ul>
</template>

<style>
body {
  background-color: #0d1117;
  color: #f0f6fc;
  min-height: 100vh;
  padding: 20px;
}
</style>