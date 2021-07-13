<template>
  <div id="app">
    <header class="d-flex justify-content-end">
      <SearchBar @searchKeyUp="searchForElement" class="m-3"/>
    </header>
    <main>
      <CardList :searched="searchArray"/>
    </main>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import SearchBar from '@/components/SearchBar.vue'
import CardList from '@/components/CardList.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    SearchBar,
    CardList
  },
  data(){
    return {
      apiLinkSearchMovies :"https://api.themoviedb.org/3/search/movie",
      api_key : '7e7faac1db87ee1385f5258c9fdad986',
      query : '',
      searchArray : '',
      language : 'it-IT'
    }
  },
  // created(){
  //   this.library();
  // },
  methods: {

    libraryMovies(){
      axios
      .get(this.apiLinkSearchMovies, {
        params : {
          api_key : this.api_key,
          query : this.query,
          language : this.language
        }
      })
      .then(rensponse=>{
        this.searchArray = rensponse.data.results;
      })
      .catch(function () {
          console.log('è vuoto');
      });
    },

    searchForElement(ele){
      if(ele.length >0) {
        this.query = ele
        this.libraryMovies();
      }
    }

  }
}
</script>

<style lang="scss">
@import '@/style/commons.scss';
#app {
  header {
    background-color: #1b1b1b;
  }
}
</style>
