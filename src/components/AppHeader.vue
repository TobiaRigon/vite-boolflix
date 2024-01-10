<script >

import axios from 'axios';
import { store } from '../store';

import AppMain from './AppMain.vue';

export default {
  name: "AppHeader",

  components: {
    AppMain,
  },

  data() {
    return {
      store,
      searchTerm: '',
      searchResults: [],
    }
  },

  methods: {
    searchMovies() {


      let myURL = `${store.apiURL}${store.apiKey}&query=${this.searchTerm}`;

      // Log aggiuntivo per verificare il valore di myURL
      console.log('myURL:', myURL);

      axios.get(myURL)
        .then(response => {
          this.searchResults = response.data.results;
          console.log(this.searchResults);
        })
        .catch(error => {
          console.error("Errore durante la ricerca di film:", error);
        });
    },




  },

};

</script>

<template>
  <header>
    <div class="search-bar">
      <input v-model="searchTerm" placeholder="Cerca film o serie TV" />
      <button @click="searchMovies">Cerca</button>
    </div>
  </header>
</template>

<style scoped></style>
