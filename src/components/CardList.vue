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
            halfStar : 'fas fa-star-half',
            emptyStar : 'far fa-star',
            fullStar : 'fas fa-star'
        }   
    },
    watch : {
        searchedMovies : {
            handler() {
                this.searchedMovies.map((element)=>{
                    this.addstar(element);
                    return element.vote_average
                });
            }
        },
        searchedTv : {
            handler() {
                this.searchedTv.map((element)=>{
                    this.addstar(element);
                    return element.vote_average
                })  
            }
        }

    },
    methods : {
        addstar(element) {
            if(element.vote_average % 2 == 0){

                this.starsShow = element.vote_average/2;
                element.vote_average = [];

                for(let i = 0;i < 5 ;i++) {
                    if(i < this.starsShow) {
                        element.vote_average.push(this.fullStar);
                    } else {
                        element.vote_average.push(this.emptyStar);
                    }
                }
            } else {
                this.starsShow = parseInt(element.vote_average/2);
                element.vote_average = [];
                for(let i = 0;i < 5 ;i++) {

                    if(i < this.starsShow) {
                        element.vote_average.push(this.fullStar);
                    }else if(i < this.starsShow +1) {
                        element.vote_average.push(this.halfStar);
                    } else  {
                        element.vote_average.push(this.emptyStar);
                    }
                }
            }
            return element.vote_average
        }
    }
}
</script>

<style scoped>

    
</style>