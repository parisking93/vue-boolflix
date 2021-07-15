<template>
    <div class="box-loader text-light">
        <i class="loader fas fa-circle-notch"></i>
    </div>
</template>

<script>
export default {
    name : 'Loader'
}
</script>

<style lang="scss" scoped>
    // scritto senza bootstrap per riutilizzo
    .box-loader {
        height: 60vh;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 50px;

        .loader{
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            from {transorm: rotate(0deg);}
            to {transform:rotate(360deg)}
        }
    }
</style>