<template>
    <div class="crumb-container">
        <div class="crumb-container-inner">
            <img src="@/static/icons/amp_stories-black-18dp.svg" />
            <div>
            <span class="crumb-id">{{data.id}}</span>
            <span class="crumb-title">{{data.name}}</span>
            </div>
            <img class="delete-button" @click="deleteCrumb" src="@/static/icons/close-24px.svg" alt="delete" />
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            data: {},
        };
    },
    props: {
        data: {
            type: Object,
            default: {},
            required: true,
        },
    },
    methods: {
    deleteCrumb(e) {
      this.$emit("deleteCrumb");
    }
  }
}
</script>

<style lang="scss" scoped>

@import "@/static/css/form-styles.scss";

.crumb-container {
    
    clear: both;
    margin: 5px 0;
    padding: 5px;
    border: 1px solid var(--interfaceItemsBorderColor);
    border-radius: var(--interfaceBorderRadius);
    &:hover {
        box-shadow: 0 2px 5px -2px var(--normalShadowColor);
    }

    .crumb-container-inner {
        display: flex;
        align-items: center;
        margin: 2px;
        justify-content: space-between;

        img, span {
            margin: 0 10px;
        }
        
        .delete-button {
            cursor: pointer;

            &:hover {
                background-color: var(--interfaceSecondaryHoverColor);
                border-radius: 50px;
                transition: .5s;
            }
        }

        .crumb-title {
            font-weight: 700;
        }
    }
    
}


</style>