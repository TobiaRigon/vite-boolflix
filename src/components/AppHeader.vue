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
    <img class="logo" src="/bootstrap_logo.png" alt="bootstrap logo">
    <div class="search-bar">
      <input @keyup.enter="$emit('SearchMedia', searchTerm)" v-model="searchTerm" placeholder="Cerca film o serie TV" />

    </div>
  </header>
</template>

<style lang="scss" scoped>
header {
  height: 80px;
  background-color: black;
  display: flex;
  justify-content: space-between;
  align-items: center;
  filter: drop-shadow(0px 3px 4px #000000);

  .logo {

    padding-left: 40px;
    height: 50px;

  }

  .search-bar {
    padding-right: 40px;

    input {
      background-color: rgb(220, 220, 220);
      font-size: 20px;
    }



  }
}
</style>
