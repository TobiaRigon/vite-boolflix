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


};

</script>

<template>
  <header>
    <div class="search-bar">
      <input v-model="searchTerm" placeholder="Cerca film o serie TV" />
      <button @click="$emit('SearchMedia', searchTerm)">Cerca</button>
    </div>
  </header>
</template>

<style scoped></style>
