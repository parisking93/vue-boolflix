<template>
    <div @mouseover="description" @mouseleave="copertinaImg" class="positon-relative">
        <div :class="hoverCard ? 'back':'front'" class="position-absolute top-0 cards-down">
            <div class="position-relative  card-library rounded-3">
                <img class="copertina w-100 h-100 rounded-3" v-if="elementCard.poster_path != null" :src="urlImgBefore + elementCard.poster_path" :alt="elementCard.name || elementCard.title">
                <div v-else  class="p-3">
                    <span class="text-capitalize display-6 text-wrap">Copertina non dispondibile</span> 
                </div>
            </div>
        </div>
        <div :class="hoverCard ? 'front': 'back'" class='position-absolute top-0 cards-down'>
            <ul class="position-relative card-library rounded-3 text-wrap p-3" >
                <li><strong>titolo originale : </strong> {{elementCard.original_name || elementCard.original_title}}</li>
                <li><strong>titolo : </strong> {{elementCard.name || elementCard.title}}</li>
                <li>
                    <strong>lingua : </strong>
                    <img v-if="elementCard.original_language == 'ja' " :src="elementFlag + 'jp' + elementSvg" width="30" :alt="elementCard.original_language"> 
                    <img v-else-if="elementCard.original_language =='en'" :src="elementFlag + 'gb' + elementSvg" width="30" :alt="elementCard.original_language">
                    <img v-else :src="elementFlag + elementCard.original_language + elementSvg" width="30" :alt="elementCard.original_language"> 

                </li>
                <li><strong>voto :  </strong>
                    <div v-for="(element,index) in elementCard.vote_average" :key="index" class="d-inline-block">
                            <div v-if="element == 'fas fa-star-half'"  class="box-star position-relative d-inline-block" >
                                <i class="position-absolute  far far fa-star"></i>
                                <i class="position-absolute" :class="element"></i>
                            </div>
                            <div v-else class="box-star position-relative d-inline-block">
                                <i class="position-absolute" :class="element"></i>
                            </div>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>

export default {
    name : 'Card',
    props : ['elementCard','elementFlag','elementSvg','urlImgBefore'],
    data() {
        return {
            hoverCard : false
        }
    },
    methods: {
        description(){
            this.hoverCard = true;
        },
        copertinaImg() {
            this.hoverCard = false;
        }
    }
}
</script>

<style lang="scss" scoped>

    .copertina {
        object-fit: cover;
        object-position: center;
    }
    .cards-down {
        transition: all 0.5s linear;
        cursor: pointer;
    }
    .back {
        opacity: 0;
    }
    .front {
        opacity: 1;
    }
    .card-library {
        width: 310px;
        height: 470px;
        overflow: hidden;
        background-color: rgba($color: #3d3b3b, $alpha: 1);
    }

</style>
