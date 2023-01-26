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
          const movies = res.data.results;
          const filteredMovies = movies.map((movie) => {
            const { title, original_title, original_language, overview, vote_average } = movie
            return { title, originalTitle: original_title, language: original_language, desc: overview, rating: vote_average }
          })

          this.moviesList = filteredMovies
        })
        .catch(err => { console.error(err) })
    },

    renderFlag(lang) {
      const url = new URL(`./assets/img/flags/${lang}.png`, import.meta.url);
      return url.href;
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
    <li v-for="movie in moviesList" :key="movie.id">
      {{ movie.title }},
      {{ movie.originalTitle }},
      <span>lang: {{ movie.language }}</span>
      <figure v-if="movie.language == 'it' || movie.language == 'en'">
        <img :src="renderFlag(movie.language)" alt="">,
      </figure>
      <p>{{ movie.desc || 'No description' }}</p>,
      {{ movie.rating }}
    </li>
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