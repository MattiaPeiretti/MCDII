<template>
    <div class='info-iframe-container'>
        <collapsable-panel class="panel" ref="collapsablePanel" title="Info" :allowDrag="true" :allowFullscreen="true" :allowClose="true" v-on:closecurrentpanel="closeCurrentPanel()">
            <iframe ref="infoIframe" style="" :src="currentURL" frameborder="0"></iframe>
        </collapsable-panel>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            infoIframe: undefined,
        }
    },
    props: {
        currentURL: {
            type: String,
            default: "",
            required: true,
            immediate: true,
            handler (val, oldVal) {
                alert();
                this.$refs.infoIframe.contentWindow.location.reload();
                console.log(newVal, oldVal);
            }
        }
    },
    methods: {
        closeCurrentPanel(e) {
            this.$emit("closecurrentpanel");

        }
    },
    mounted() {
        this.$refs.infoIframe.contentWindow.location.reload();
    }

    
}
</script>

<style lang="scss" scoped>
    iframe{
        width: 100%;
        height: 100%;
        min-height: 30vh;
    }

    
</style>