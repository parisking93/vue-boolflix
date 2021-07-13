<template>
    <div>
        <div v-if="!elementSearched" class="container" >

        </div>
        <div class="container" v-else>
            <h4>Films trovati per : {{elementSearched}}</h4>
            <div class="d-flex flex-wrap overflow-x-hidden">
                <div v-for="element in searchedMovies"  :key="element.id" >
                    <CardMovie :elementMovie ="element" :elementFlag="flag" :elementSvg="svg"/>
                </div>
            </div>


            <h4>Serie Tv trovate per : {{elementSearched}}</h4>
            <div class="d-flex flex-wrap overflow-x-hidden">
                <div v-for="element in searchedTv"  :key="element.id"  >
                <CardTv :elementTv ="element" :elementFlag="flag" :elementSvg="svg"/>
                </div>
            </div>
            
        </div>


    </div>


</template>

<script>
import CardMovie from '@/components/CardMovie.vue'
import CardTv from '@/components/CardTv.vue'

export default {
    name:'CardLists',
    components : {
        CardMovie,
        CardTv
    },
    props : ['searchedMovies','searchedTv','elementSearched'],
    data() {
        return {
            flag :  'https://flagcdn.com/',
            svg : '.svg',
        }   
    },
}
</script>

<style scoped>
    
</style>