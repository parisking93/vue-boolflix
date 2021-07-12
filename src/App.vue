<template>
  <div id="app">
    <header>
      <SearchBar @searchKeyUp="searchForElement"/>
    </header>
    <main>

    </main>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import SearchBar from '@/components/SearchBar.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    // HelloWorld
    SearchBar
  },
  data(){
    return {
      apiLinkSearchMovies :"https://api.themoviedb.org/3/search/movie",
      api_key : '7e7faac1db87ee1385f5258c9fdad986',
      query : 'matrix'
    }
  },
  created(){
    this.library();
  },
  methods: {

    library(){
      axios
      .get(this.apiLinkSearchMovies, {
        params : {
          api_key : this.api_key,
          query : this.query
        }
      })
      .then(rensponse=>{
        console.log(rensponse.data);
      })
      .catch(function (error) {
          console.log(error);
      });
    },

    searchForElement(ele){
      console.log(ele);
      this.query = ele
      this.library()
      console.log(this.query);
    }

  }
}
</script>

<style lang="scss">
@import '@/style/commons.scss';
#app {
  // font-family: Avenir, Helvetica, Arial, sans-serif;
  // -webkit-font-smoothing: antialiased;
  // -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  // color: #2c3e50;
  // margin-top: 60px;
}
</style>
