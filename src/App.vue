<script>
import axios from 'axios';
import { apiUri, apiKey, imgUri } from './data'
export default {
  name: 'Boolflix',
  data() {
    return {
      searchWord: '',
      moviesList: [],
      showsList: [],
      imgUri
    }
  },
  methods: {
    // get movies&shows by name from the API
    fetchMovies() {
      // verify if input is not valid
      if (!this.searchWord) return

      //get movies from api with selected keys
      axios.get(`${apiUri}/search/movie?api_key=${apiKey}&query=${this.searchWord}`)
        .then(res => {
          //put the result in a variable
          const movies = res.data.results;

          // filter the result by giving a new array with selected keys
          const filteredMovies = movies.map((movie) => {
            let { title, original_title, original_language, overview, vote_average, poster_path } = movie;

            vote_average = Math.ceil(vote_average / 2);

            return { title, originalTitle: original_title, language: original_language, desc: overview, rating: vote_average, bannerUrl: poster_path }
          })

          //push the new array in data
          this.moviesList = filteredMovies
        })
        .catch(err => { console.error(err) });

      //get shows from api with selected keys
      axios.get(`${apiUri}/search/tv?api_key=${apiKey}&query=${this.searchWord}`)
        .then(res => {
          //put the result in a variable
          const shows = res.data.results;

          // filter the result by giving a new array with selected keys
          const filteredShows = shows.map((show) => {
            const { name, original_name, original_language, overview, vote_average, poster_path } = show
            return { title: name, originalTitle: original_name, language: original_language, desc: overview, rating: vote_average, bannerUrl: poster_path }
          })

          //push the new array in data
          this.showsList = filteredShows
        })
        .catch(err => { console.error(err) });
    },

    //build the url for the flag image
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

  <!-- # Movies&Shows list -->
  <ul>
    <h1>----------------FILM---------------</h1>
    <li v-for="movie in moviesList" :key="movie.id">
      <!-- banner image -->
      <img :src="`${imgUri}${movie.bannerUrl}`" alt="">

      <!-- title -->
      {{ movie.title }},

      <!-- original title -->
      {{ movie.originalTitle }},

      <!-- if it or en, language flag -->
      <span>lang: </span>
      <figure v-if="movie.language == 'it' || movie.language == 'en'">
        <img :src="renderFlag(movie.language)" alt="">,
      </figure>

      <!-- language -->
      <span v-else>{{ movie.language }}</span>

      <!-- desc -->
      <p>{{ movie.desc || 'No description' }}</p>,

      <!-- rating -->
      {{ movie.rating }}
    </li>
    <br>
    <hr>
    <br>
    <h1>----------------SERIES---------------</h1>
    <li v-for="show in showsList" :key="show.id">
      <!-- banner image -->
      <img :src="`${imgUri}${show.bannerUrl}`" alt="">

      <!-- title -->
      {{ show.title }},

      <!-- original title -->
      {{ show.originalTitle }},

      <!-- language -->
      <span>lang: {{ show.language }}</span>

      <!-- if it or en, language flag -->
      <figure v-if="show.language == 'it' || show.language == 'en'">
        <img :src="renderFlag(show.language)" alt="">,
      </figure>

      <!-- desc -->
      <p>{{ show.desc || 'No description' }}</p>,

      <!-- rating -->
      {{ show.rating }}
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