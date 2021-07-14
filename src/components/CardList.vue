<template>
    <div class="contenitore w-100 h-100 overflow-auto text-light">
        <div v-if="!elementSearched" >
        </div>
        <div  class="bo" v-else>
            <h3 class="mt-4 mb-3">Films trovati per : {{elementSearched}}</h3>

            <div >
                <Card v-for="element in searchedMovies" :key="element.id" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
            </div>
            <h3 class="mt-4 mb-3">Serie Tv trovate per : {{elementSearched}}</h3>
            <div>
                <Card v-for="element in searchedTv"  :key="element.id" :elementCard ="element" :elementFlag="flag" :elementSvg="svg" :urlImgBefore="preUrl"/>
            </div>
            
        </div>
        <!-- <div id="carouselExampleControls" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
                <div class="carousel-item active">
                <img src="..." class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                <img src="..." class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                <img src="..." class="d-block w-100" alt="...">
                </div>
            </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
        </div> -->
        <!-- <split-carousel class="bo">
            <split-carousel-item  class="" v-for="item in 8" :key="item">
                <div class="box">{{ item }}</div>
            </split-carousel-item >
        </split-carousel> -->


    </div>


</template>

<script>
import Card from '@/components/Card.vue'
// import { SplitCarousel, SplitCarouselItem } from "vue-split-carousel";
// import SplitCarousel from "./components/SplitCarousel.vue";
// import SplitCarouselItem from "./components/SplitCarouselItem.vue";

export default {
    name:'CardLists',
    components : {
        Card,
        // SplitCarousel,
        // SplitCarouselItem
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

</style>