<template>
  <div id="app">
    <header class="d-flex justify-content-end">
      <SearchBar @searchKeyUp="searchForElement" class="m-3"/>
    </header>
    <main class="px-5">
      <!-- <div class="text-light far fa-star"></div> -->
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
      preUrlImg : 'https://image.tmdb.org/t/p/w342',


    }
  },
  methods: {

    library(){


      const request = {
        params : {
        api_key : this.api_key,
        query : this.query,
        language : this.language
        }
      }
      axios
        .all([
          axios.get(this.apiLinkSearchMovies, request),
          axios.get(this.apiLinkSearchTv, request)
        ])
        .then(axios.spread((responseMovie, responseTV)=>{
          this.searchArrayMovies = responseMovie.data.results;
          this.searchArrayTv = responseTV.data.results;
        }))


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
@import '@/style/commonsTagsClass.scss';

#app {
  header {
    background-color: #1b1b1b;
  }
  main {
    width: 100%;
    height: calc(100vh - 62px);
    background-color: #1b1b1b;
  }

}
</style>
