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
      searchResults: [],
    }
  },



  methods: {

    searchMedia(searchTerm) {
      this.searchTerm = searchTerm;
      let tvURL = `${store.apiURL}/tv${store.apiKey}`;
      let movieURL = `${store.apiURL}/movie${store.apiKey}`;

      let myMovieURL = `${movieURL}&language=it_IT&query=${this.searchTerm}`;
      let myTvURL = `${tvURL}&language=it_IT&query=${this.searchTerm}`;

      // Log aggiuntivo per verificare il valore di myURL
      console.log('myURL:', myMovieURL, myTvURL, searchTerm);

      // Eseguire la chiamata axios per i film
      axios.get(myMovieURL)
        .then(movieResponse => {
          if (searchTerm === undefined) {
            this.searchResults = [];
          } else {
            this.searchResults = movieResponse.data.results;

            // Eseguire la seconda chiamata axios per le serie TV
            axios.get(myTvURL)
              .then(tvResponse => {
                // Aggiungere i risultati delle serie TV agli altri risultati
                this.searchResults = [...this.searchResults, ...tvResponse.data.results];
                console.log(this.searchResults, this.searchResults.length);
              })
              .catch(tvError => {
                console.error("Errore durante la ricerca di serie TV:", tvError);
              });
          }
        })
        .catch(movieError => {
          console.error("Errore durante la ricerca di film:", movieError);
        });

    },

  },


  created() {
    this.searchMedia();


  }


}

</script>

<template>
  <AppHeader @SearchMedia="searchMedia" />
  <AppMain :searchResults="searchResults" />
</template>

<style scoped></style>
