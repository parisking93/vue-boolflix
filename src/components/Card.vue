<template>
    <div>
        <div>
           <img v-if="elementCard.poster_path != null" :src="urlImgBefore + elementCard.poster_path" :alt="elementCard.name || elementCard.title">
           <div v-else>Copertina non dispondibile</div>
        </div>
        <ul>
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
</template>

<script>
export default {
    name : 'Card',
    props : ['elementCard','elementFlag','elementSvg','urlImgBefore'],

}
</script>

<style>

</style>