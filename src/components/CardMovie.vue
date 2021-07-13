<template>
    <div class="me-3">
        <div>
           <div v-if="elementMovie.poster_path == null || elementMovie.poster_path == undefined ">Copertina non dispondibile</div>
           <img  :src="urlImgBefore + elementMovie.poster_path" :alt="elementMovie.title">
        </div>
        <ul>
            <li><strong>titolo originale : </strong> {{elementMovie.original_title}}</li>
            <li><strong>titolo : </strong> {{elementMovie.title}}</li>
            <li>
                <strong>lingua : </strong>
                <img v-if="elementMovie.original_language == 'ja' " :src="elementFlag + 'jp' + elementSvg" width="30" :alt="elementMovie.original_language"> 
                <img v-else-if="elementMovie.original_language =='en'" :src="elementFlag + 'gb' + elementSvg" width="30" :alt="elementMovie.original_language"> 
                <img v-else :src="elementFlag + elementMovie.original_language + elementSvg" width="30" :alt="elementMovie.original_language"> 

            </li>
            <li><strong>voto :  </strong>
                 <div v-for="(element,index) in elementMovie.vote_average" :key="index" class="d-inline-block">
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
    name:  'CardMovie',
    props : ['elementMovie','elementFlag','elementSvg','urlImgBefore'],
}
</script>

<style lang="scss" scoped>

</style>