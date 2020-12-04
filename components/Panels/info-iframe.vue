<template>
    <div class='info-iframe-container'>
        <iframe style="width: 100%; height: 100%;" :src="currentURL" frameborder="0"></iframe>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            currentURL: "",
        }
    },
    props: {
        currentURL: {
            type: String,
            required: true,
        }
    },
    mounted() {
        
    }
    
}
</script>

<style lang="scss" scoped>
    .info-iframe-container {
        height: 100%;
    }

    iframe{
        width: 100%;
        height: 10vw;

    }
</style>