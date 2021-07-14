<template>
    <div class="contenitore w-100 h-100 overflow-auto text-light">
        <div v-if="!elementSearched" >
        </div>
        <div v-else>
            <h3 class="mt-4 mb-3">Films trovati per : {{elementSearched}}</h3>
            <div class="library d-flex flex-wrap position-relative">
                <Card v-for="element in searchedMovies"  :key="element.id" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
            </div>

            <h3 class="mt-4 mb-3">Serie Tv trovate per : {{elementSearched}}</h3>
            <div class="library d-flex flex-wrap position-relative">
                <Card v-for="element in searchedTv"  :key="element.id" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
            </div>
            
        </div>


    </div>


</template>

<script>
import Card from '@/components/Card.vue'

export default {
    name:'CardLists',
    components : {
        Card
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
                this.addstar(this.searchedMovies);
            }
        },
        searchedTv : {
            handler() {
                this.addstar(this.searchedTv);
            }
        }

    },
    methods : {
        addstar(array) {
            array.map((element)=>{
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
            });
        }
    }
}
</script>

<style lang="scss" scoped>
    // .contenitore {

    //         // .library {
    //         //     width: $casa *;
    //         // }
    // }
    
</style>