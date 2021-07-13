<template>
    <div class="d-flex flex-wrap overflow-x-hidden">
        <ul v-for="element in searched"  :key="element.id" class="m-2">
            <li><strong>titolo originale : </strong> {{element.original_title}}</li>
            <li><strong>titolo : </strong> {{element.title}}</li>
            <li>
                <strong>lingua : </strong>
                <img v-if="element.original_language !='en'" :src="flag + element.original_language + svg" width="30" :alt="element.original_language"> 

                <img v-else :src="flag + 'gb' + svg" width="30" :alt="element.original_language"> 
            </li>
            <li><strong>voto :  </strong> {{element.vote_average}}</li>
        </ul>
    </div>

</template>

<script>
export default {
    name:'CardLists',
    props : ['searched'],
    data() {
        return {
            bandiereArray : ['it','en','fr'],
            flag :  'https://flagcdn.com/',
            svg : '.svg',
        }
    },

}
</script>

<style>

</style>