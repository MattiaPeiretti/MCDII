<template>
    <div class="container-info-text" @click="clicked()">
        <p><slot></slot>&#128712; </p>
    </div>
</template>

<script>
export default {
    methods: {
        clicked() {
            this.$emit("clicked")
        }
    }
}
</script>

<style lang="scss" scoped>
    .container-info-text {
        display: inline-block;
        p {
            color: gray;
            padding-right: 5px;
            cursor: help;
        }
        margin: 0!important;
        padding: 0!important;
    }
</style>