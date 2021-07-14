<template>
  <form class="me-5">
      <i class="text-light me-3 fas fa-bell"></i>
      <input type="text" id="searchbar" v-model="searchMovie" placeholder="Cerca i tuoi film...">
      <button class="btn-dark ms-1" @click.prevent="resetSearch"><i class="fas fa-search"></i></button>
  </form>
</template>

<script>
export default {
    name : 'SearchBar',
    data() {
        return {
            searchMovie : ''
        }
    },
    methods : {
        resetSearch(){
            this.$emit('searchKeyUp', this.searchMovie)
            this.searchMovie = '';
            // emit si può richiamare all'interno di un metodo
            // this.$emit('searchForm',this.inputText);            
            
        }
    }
}
</script>

<style>

</style>
