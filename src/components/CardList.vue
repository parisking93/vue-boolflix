<template>
    <div class="h-100 text-light ps-4">
        <!-- lista iniziale card  -->

        <div v-if="!elementSearched" >
            <div v-if="!done" class="text-ligth">
                <Loader/>
            </div>
            <div v-else >
                <div v-for="genere in genreMovies" :key="genere.id">
                    <h3 class="mt-4 mb-3 ms-4 text-danger">{{genere.name}}</h3>
                    <carousel
                    :perPage='4'
                    :navigationEnabled="true"
                    :mouse-drag="false"
                    paginationColor="#d8d8d8" paginationActiveColor="#ee1414"
                    class="slider overflow-hidden ms-4">
                        <slide v-for="(element,index) in genere.arrGenere" :key="index">
                            <Card class="card-library rounded-3" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
                        </slide>
                    </carousel>
                </div> 

            </div> 

        </div>
        <div v-else>
            <!-- prima lista di card  -->

            <div v-if="searchedMovies.length != 0">
                <h3 class="mt-4 mb-3 ms-4 text-danger">Films trovati per : <span class="text-light text-uppercase">  {{elementSearched}}</span></h3>
                <carousel
                :perPage='4'
                :navigationEnabled="true"
                :mouse-drag="false"
                paginationColor="#d8d8d8" paginationActiveColor="#ee1414"
                class="slider overflow-hidden ms-4">
                    <slide v-for="(element,index) in searchedMovies" :key="index">
                        <Card class="card-library rounded-3" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
                    </slide>
                </carousel>
            </div>
            <div v-else>
                <h3 class="mt-4 mb-3 ms-4 text-danger">Non ci sono risultati per <span class="text-light text-uppercase"> {{elementSearched}} </span></h3>
            </div>
            <!-- seconda lista di card  -->
            <div v-if="searchedTv.length != 0">
                <h3 class="mt-4 mb-3 ms-4 text-danger">Serie Tv trovate per : <span class="text-light text-uppercase">  {{elementSearched}}</span></h3>
                <carousel
                    :perPage='4'
                    :navigationEnabled="true"
                    :mouse-drag="false"
                    paginationColor="#d8d8d8" paginationActiveColor="#ee1414"
                    class="slider overflow-hidden ms-4">
                        <slide v-for="(element,index) in searchedTv" :key="index">
                            <Card  class="card-library rounded-3" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
                        </slide>
                </carousel>
            </div>
            <div v-else>
                <h3 class="mt-4 mb-3 ms-4 text-danger">Non ci sono risultati per <span class="text-light text-uppercase"> {{elementSearched}} </span></h3>
            </div>

        </div>
         <!-- <div v-for="(element, index) in discoverMovies" :key="index">
         </div> -->
    </div>


</template>

<script>
import Card from '@/components/Card.vue'
import { Carousel, Slide } from 'vue-carousel';
import Loader from '@/components/Loader.vue';


export default {
    name:'CardLists',
    components : {
        Card,
        Carousel,
        Slide,
        Loader
    },
    props : ['searchedMovies','searchedTv','elementSearched','preUrl','genreMovies'],
    data() {
        return {
            flag :  'https://flagcdn.com/',
            svg : '.svg',
            halfStar : 'fas fa-star-half',
            emptyStar : 'far fa-star',
            fullStar : 'fas fa-star',
            done : false,
        }   
    },
    watch : {
        genreMovies : {
            handler() {
                if(this.genreMovies.length > 1) {
                    setTimeout(()=>{
                        this.done = true
                    },1000)
                }
            }
        },
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
        },
        addstarS(array) {
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
        },

    }
}
</script>

<style lang="scss" scoped>


.slider {
        width: calc(100vw - 50px);
    }
</style>