<script >
import axios from 'axios';
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'


import { store } from './store';

export default {
  components: {
    AppHeader,
    AppMain,
  },

  data() {
    return {
      store,
    }
  },
  methods: {

    searchMovies(searchTerm) {
      this.searchTerm = searchTerm;
      let myURL = `${store.apiURL}${store.apiKey}&query=${this.searchTerm}`;

      // Log aggiuntivo per verificare il valore di myURL
      console.log('myURL:', myURL, searchTerm);

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


  created() {
    this.searchMovies();


  }


}

</script>

<template>
  <AppHeader @SearchMovies="searchMovies" />
  <AppMain />
</template>

<style scoped></style>
