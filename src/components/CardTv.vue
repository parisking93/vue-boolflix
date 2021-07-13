<template>
    <div>
        <ul>
            <li><strong>titolo originale : </strong> {{elementTv.original_name}}</li>
            <li><strong>titolo : </strong> {{elementTv.name}}</li>
            <li>
                <strong>lingua : </strong>
                <img v-if="elementTv.original_language == 'ja' " :src="elementFlag + 'jp' + elementSvg" width="30" :alt="elementTv.original_language"> 
                <img v-else-if="elementTv.original_language =='en'" :src="elementFlag + 'gb' + elementSvg" width="30" :alt="elementTv.original_language">
                <img v-else :src="elementFlag + elementTv.original_language + elementSvg" width="30" :alt="elementTv.original_language"> 

            </li>
            <li><strong>voto :  </strong> {{elementTv.vote_average}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name : 'CardTv',
    props : ['elementTv','elementFlag','elementSvg'],

}
</script>

<style>

</style>