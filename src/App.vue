<template>
  <div id="app">
    <header class="d-flex  justify-content-between align-items-center">
      <Logo/>
      <SearchBar @searchKeyUp="searchForElement" class="m-3"/>
    </header>
    <main class="overflow-hidden">
      <CardList class="overflow-auto h-100" :genreMovies="genreArray" :searchedMovies="searchArrayMovies" :searchedTv="searchArrayTv" :elementSearched="query" :preUrl="preUrlImg"/>
    </main>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import SearchBar from '@/components/SearchBar.vue';
import Logo from '@/components/Logo.vue';
import CardList from '@/components/CardList.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    SearchBar,
    CardList,
    Logo
  },
  data(){
    return {
      apiLinkSearchMovies :"https://api.themoviedb.org/3/search/movie",
      apiLinkSearchTv : "https://api.themoviedb.org/3/search/tv",
      apiLinkGenre : "https://api.themoviedb.org/3/genre/movie/list",
      apiLinkDiscover : "https://api.themoviedb.org/3/discover/movie",
      api_key : '7e7faac1db87ee1385f5258c9fdad986',
      query : '',
      searchArrayMovies : '',
      searchArrayTv : '',
      language : 'it-IT',
      preUrlImg : 'https://image.tmdb.org/t/p/w342',
      genreArray : [],
      discoverArray : [],
      popularity : 'popularity.desc',

    }
  },
  created(){

      
      // api per la schermata iniziale genere e discover
      axios
        .get(this.apiLinkDiscover, {
          params : {
            api_key : this.api_key,
            sort_by : this.popularity
          }
        })
        .then(rensponse => {
          this.discoverArray = rensponse.data.results
          let newElement = {
            id : 1,
            name : 'Nuove Uscite',
            arrGenere : this.discoverArray
          }
          this.genreArray.unshift(newElement)

        });
        axios
        .get(this.apiLinkGenre, {
          params : {
            api_key : this.api_key,
            language : this.language
          }
        })
        .then(rensponse => {
          this.genreArray = rensponse.data.genres;
        });


    
  },
  watch : {
    genreArray : {
      handler() {
        this.genreArray.map((element) =>{
          if(!element.arrGenere) {
            axios
              .get(this.apiLinkDiscover, {
                params : {
                  api_key : this.api_key,
                  with_genres : element.id,
                  language : this.language
                }
              })
              .then(rensponse => {
                 return element.arrGenere = rensponse.data.results
              });
          }
        });
      }
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
    background-color: #2d2b2b;
    height: 80px;

  }
  main {
    height: calc(100vh - 80px);
    background-color: #1b1b1b;
  }

}
</style>
