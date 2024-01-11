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
    <div class="logo">
      BOOTFLIX
    </div>
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
    color: red;
    padding-left: 40px;
    font-size: 35px;
    font-weight: bold;
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
