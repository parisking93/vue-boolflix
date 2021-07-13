<template>
    <div class="container text-light">
        <div v-if="!elementSearched"  >

        </div>
        <div v-else>
            <h3 class="mt-4 mb-3">Films trovati per : {{elementSearched}}</h3>
            <div class="d-flex flex-wrap">
                <div v-for="element in searchedMovies"  :key="element.id" >
                    <CardMovie :elementMovie ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
                </div>
            </div>


            <h3 class="mt-4 mb-3">Serie Tv trovate per : {{elementSearched}}</h3>
            <div class="d-flex flex-wrap">
                <div v-for="element in searchedTv"  :key="element.id"  >
                <CardTv :elementTv ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
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
    props : ['searchedMovies','searchedTv','elementSearched','preUrl'],
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