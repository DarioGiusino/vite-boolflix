<script>
import axios from 'axios';
import { apiUri, apiKey, imgUri } from './data';
import { store } from './data/store';
import AppHeader from './components/AppHeader.vue';
export default {
  name: 'Boolflix',
  data() {
    return {
      store,
      searchWord: '',
      imgUri
    }
  },
  components: { AppHeader },
  computed: {
    APIConfig() {
      return {
        params: {
          api_key: apiKey,
          query: this.searchWord
        }
      }
    }
  },

  methods: {
    // get movies&shows by name calling API
    fetchPrograms() {
      // verify if input is not valid
      if (!this.searchWord) {
        store.moviesList = [];
        return
      }

      this.callAPI('search/movie', 'moviesList');
      this.callAPI('search/tv', 'showsList');
    },

    // call API by giving and endpoint and a variable where to store the data
    callAPI(endpoint, collection) {
      //get shows from api with selected keys
      axios.get(`${apiUri}/${endpoint}`, this.APIConfig)
        .then(res => {
          //put the result in a variable
          const programs = res.data.results;

          // filter the result by giving a new array with selected keys
          const filteredPrograms = programs.map((program) => {
            let { name, title, original_title, original_name, original_language, overview, vote_average, poster_path } = program;

            vote_average = Math.ceil(vote_average / 2);

            return { title: name || title, originalTitle: original_name || original_title, language: original_language, desc: overview, rating: vote_average, bannerUrl: poster_path }
          })

          //push the new array in data
          store[collection] = filteredPrograms
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
  <app-header></app-header>

  <!-- # Movies&Shows list -->
  <ul>
    <h1>----------------FILM---------------</h1>
    <li v-for="movie in store.moviesList" :key="movie.id">
      <!-- banner image -->
      <span v-if="!movie.bannerUrl">-No banner-</span>
      <img v-else :src="`${imgUri}${movie.bannerUrl}`" alt="">

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
    <li v-for="show in store.showsList" :key="show.id">
      <!-- banner image -->
      <span v-if="!show.bannerUrl">-No banner-</span>
      <img v-else :src="`${imgUri}${show.bannerUrl}`" alt="">

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
}
</style>