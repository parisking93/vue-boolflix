<template>
    <div class="me-3">
        <div>
           <img v-if="elementMovie.poster_path != null" :src="urlImgBefore + elementMovie.poster_path" :alt="elementMoviei.name">
           <div v-else>Copertina non dispondibile</div>
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
            <li><strong>voto :  </strong> {{elementMovie.vote_average}}</li>
        </ul>
    </div>
</template>


<script>
export default {
    name:  'CardMovie',
    props : ['elementMovie','elementFlag','elementSvg','urlImgBefore'],
}
</script>

<style>

</style>