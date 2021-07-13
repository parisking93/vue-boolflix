<template>
  <div id="app">
    <header class="d-flex justify-content-end">
      <SearchBar @searchKeyUp="searchForElement" class="m-3"/>
    </header>
    <main>
      <CardList :searchedMovies="searchArrayMovies" :searchedTv="searchArrayTv" :elementSearched="query" :preUrl="preUrlImg"/>
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
      apiLinkSearchTv : "https://api.themoviedb.org/3/search/tv",
      api_key : '7e7faac1db87ee1385f5258c9fdad986',
      query : '',
      searchArrayMovies : '',
      searchArrayTv : '',
      language : 'it-IT',
      preUrlImg : 'https://image.tmdb.org/t/p/w342'
    }
  },
  methods: {

    library(){
      axios
      .get(this.apiLinkSearchMovies, {
        params : {
          api_key : this.api_key,
          query : this.query,
          language : this.language
        }
      })
      .then(rensponse=>{
        this.searchArrayMovies = rensponse.data.results;
      })
      .catch(function () {
          console.log('è vuoto');
      });
      axios
      .get(this.apiLinkSearchTv, {
        params : {
          api_key : this.api_key,
          query : this.query,
          language : this.language
        }
      })
      .then(rensponse=>{
        this.searchArrayTv = rensponse.data.results;
      })
    },

    searchForElement(ele){
      if(ele.length >0) {
        this.query = ele
        this.library();
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
  main {
    height: calc(100vh - 62px);
    background-color: #1b1b1b;
    overflow: auto;
  }

}
</style>
