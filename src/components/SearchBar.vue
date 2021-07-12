<template>
  <form>
      <label for="searchbar">cerca</label>
      <input type="text" id="searchbar" v-model="searchMovie" >
      <button @click.prevent="$emit('searchKeyUp', searchMovie)">Cerca</button>
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