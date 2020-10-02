<template>
    <div class="layer-editor-container">
        <div class="controls">
        <button @click="isModalOpened = !isModalOpened">Add New Layer</button>
        <button>Clear All</button>
        </div>
        <div v-if="isModalOpened" class="layer-editor-modal">
            <div class="layer-editor-modal-inner">
                <p>Choose layer type: 
                    <select>
                        <option>test1</option>
                        <option>test1</option>
                        <option>test1</option>
                        <option>test1</option>
                    </select><br>
                </p>
                <button @click="isModalOpened=false">Cancel</button>
                <button>Create</button>
            </div>
            
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isModalOpened: false,
        }
    }
}
</script>

<style lang="scss" scoped>

.layer-editor-container {
    position: relative;
    width: 100%;
    min-height: 100px;
}

.layer-editor-modal {
    background-color: rgba($color: #000000, $alpha: 0.2);
    backdrop-filter: blur(1px);
    
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100px;
    

    .layer-editor-modal-inner {
        background-color: var(--interfaceBackgroundColor);
        width: 80%;
        box-shadow: 0 2px 5px -2px var(--normalShadowColor);
        border-radius: var(--interfaceBorderRadius);
        padding: 10px;
    }
}

</style>