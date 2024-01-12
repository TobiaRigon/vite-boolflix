<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
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
      searchTerm: '',
      loading: true,
    };
  },

  methods: {
    getRandomLetter() {
      const alphabet = 'abcdefghijklmnopqrstuvwxyz';
      const randomIndex = Math.floor(Math.random() * alphabet.length);
      return alphabet[randomIndex];
    },

    getRandomNumber(n) {
      return Math.floor(Math.random() * n) + 1;
    },

    hideLoader() {
      // Nascondi il loader dopo un breve ritardo
      setTimeout(() => {
        this.loading = false;
      }, 500); // Puoi regolare la durata del ritardo in millisecondi
    },


    searchMedia(searchTerm) {
      this.loading = true;
      this.searchTerm = searchTerm;
      let tvURL = `${store.apiURL}/tv${store.apiKey}`;
      let movieURL = `${store.apiURL}/movie${store.apiKey}`;

      let myMovieURL = `${movieURL}&language=it_IT&query=${this.searchTerm}`;
      let myTvURL = `${tvURL}&language=it_IT&query=${this.searchTerm}`;

      axios.get(myMovieURL)
        .then(movieResponse => {
          if (searchTerm === undefined) {
            this.searchResults = [];
          } else {
            this.searchResults = movieResponse.data.results;

            axios.get(myTvURL)
              .then(tvResponse => {
                this.searchResults = [...this.searchResults, ...tvResponse.data.results];
                console.log(this.searchResults, this.searchResults.length);
                this.hideLoader()
              })
              .catch(tvError => {
                console.error("Errore durante la ricerca di serie TV:", tvError);
                this.hideLoader()
              });
          }
        })
        .catch(movieError => {
          console.error("Errore durante la ricerca di film:", movieError);
          this.hideLoader()
        });
    },

    startSearch() {
      this.loading = true;
      let letterSearch = this.getRandomLetter();
      let randomPage = this.getRandomNumber(10);
      let startURL = `${store.apiURL}/movie${store.apiKey}`;
      let myStartURL = `${startURL}&language=it_IT&page=${randomPage}&query=${letterSearch}&adult=false`;

      axios
        .get(myStartURL)
        .then(response => {
          this.searchResults = response.data.results;
          console.log(myStartURL);
          this.hideLoader()
        })
        .catch(error => {
          console.error('Errore durante la ricerca di film:', error);
          this.hideLoader()
        });
    },
  },

  created() {
    this.startSearch();

  },
};
</script>

<template>
  <AppHeader @SearchMedia="searchMedia" />
  <AppMain :searchResults="searchResults" :startSearchProp="startSearch" :loading="loading" />
</template>

<style scoped></style>
