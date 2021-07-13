<template>
  <form>
      <i class="text-light me-3 fas fa-bell"></i>
      <input type="text" id="searchbar" v-model="searchMovie" placeholder="Cerca i tuoi film...">
      <button class="btn-dark ms-1" @click.prevent="$emit('searchKeyUp', searchMovie)"><i class="fas fa-search"></i></button>
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
    
}
</script>

<style>

</style>
