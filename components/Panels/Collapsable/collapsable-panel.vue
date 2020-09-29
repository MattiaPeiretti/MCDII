<template>
    <div class="container">
    <div class="header">
        <button class="open-fold-button" @click="isOpened = !isOpened">{{isOpened ? 'Close' : 'Open'}}</button>
        <h3>{{title}}</h3>
    </div>

        <div class="content" v-if="isOpened"><slot></slot></div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isOpened: false,
        };
    },
    props: {
        title: {
            type: String,
            required: true,
        }
    }
}
</script>

<style lang="scss" scoped>

.container {
    box-shadow: 0 2px 5px -2px rgba(0, 0, 0, 0.2);
    margin: 10px;
    border: 1px solid #eee;
    border-radius: 15px 15px 0px 0px;
    

    .header {
        display: flex;
        align-items: center;
        background-color: #eee;
        border-radius: 15px 15px 0px 0px;
        border: 1px solid #eee;
        height: 50px;

        button {
            background: transparent;
            border: none;
            cursor: pointer;
        }

        button:focus {
            outline: none;
        }
        
    }

    .content {
        padding: 10px;
    }
}

</style>