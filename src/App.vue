<script>
import axios from 'axios';
import { apiUri, apiKey, imgUri } from './data';
import { store } from './data/store';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
export default {
  name: 'Boolflix',
  data() {
    return {
      store,
      searchWord: '',
      imgUri
    }
  },

  components: { AppHeader, AppMain },

  computed: {
    //build a query string for axios call as an object
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
    //updating the searchWord in data with the one from the searchBar
    getSearchedWord(word) {
      this.searchWord = word
    },

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

            //round the vote
            vote_average = Math.ceil(vote_average / 2);

            return { title: name || title, originalTitle: original_name || original_title, language: original_language, desc: overview, rating: vote_average, bannerUrl: poster_path }
          })

          //push the new array in data
          store[collection] = filteredPrograms
        })
        .catch(err => { console.error(err) });
    }
  }
}
</script>

<template>
  <!-- # header -->
  <app-header @search-programs="fetchPrograms" @writing-word="getSearchedWord"></app-header>

  <!-- # Movies&Shows list -->
  <app-main></app-main>


</template>

<style lang="scss">
@use './assets/scss/style.scss'
</style>