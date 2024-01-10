<script >

import axios from 'axios';
import { store } from '../store';

export default {
  name: "AppHeader",

  data() {
    return {
      store,
      searchTherm: '',
    }
  },

  methods: {
    searchMovies() {

      // axios
      //     .get(store.arcURL)

      //     .then((res) => {
      // const archetypes = res.data.slice(0, 30).map(item => item.archetype_name);
      // store.archetypes = archetypes;
      // console.log(archetypes);
      //     })
      //     .catch((err) => {
      //       console.log('Errori', err);
      //     });

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
