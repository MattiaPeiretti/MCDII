<template>
<div ref="draggable" class="container-outer" :class="{
          'fullscreen': isFullscreen,
          'anchored': isAnchored,
          'unanchored': !isAnchored,
        }">
    <div class="container">
        <div class=" header">
            <div v-if="!isFullscreen&&allowCollapse" @click="isOpened = !isOpened" class="arrow" :class="{
          'arrow-down': isOpened}">
            </div>
            <h3>{{ title }}</h3>
            <div :class="{'hidden': isAnchored}" class='draggable-header' ref="draggableHeader"></div>
            <div v-if="allowDrag || allowFullscreen || allowClose" class="buttons">
                <img v-if="!isFullscreen&&isAnchored&&allowDrag" @click='isAnchored= !isAnchored' src="@/static/icons/picture_in_picture-24px.svg" alt="">
                <img v-if="!isFullscreen&&!isAnchored&&allowDrag" @click='isAnchored= !isAnchored' src="@/static/icons/view_agenda-24px.svg" alt="">
                <img v-if="isAnchored&&!isFullscreen&&allowFullscreen" @click='isFullscreen= !isFullscreen' src="@/static/icons/open_in_full-24px.svg" />
                <img v-if="isAnchored&&isFullscreen&&allowFullscreen" @click='isFullscreen= !isFullscreen' src="@/static/icons/close_fullscreen-24px.svg" />
                <img v-if="allowClose" @click='closePanelMethod()' src="@/static/icons/close-24px.svg" />
            </div>
        </div>

        <div ref="content" class="content" :class="{
        'content-opened': isOpened,
      }">
            <slot></slot>
        </div>
    </div>
</div>
</template>

<script>
function dragElement(element, header) {
    const elmnt = element;

    var pos1 = 0,
        pos2 = 0,
        pos3 = 0,
        pos4 = 0;
    if (header) {
        // if present, the header is where you move the DIV from:
        header.onmousedown = dragMouseDown;
    } else {
        // otherwise, move the DIV from anywhere inside the DIV:
        elmnt.onmousedown = dragMouseDown;
    }

    function dragMouseDown(e) {
        e = e || window.event;
        e.preventDefault();
        // get the mouse cursor position at startup:
        pos3 = e.clientX;
        pos4 = e.clientY;
        document.onmouseup = closeDragElement;
        // call a function whenever the cursor moves:
        document.onmousemove = elementDrag;
    }

    function elementDrag(e) {
        e = e || window.event;
        e.preventDefault();
        // calculate the new cursor position:
        pos1 = pos3 - e.clientX;
        pos2 = pos4 - e.clientY;
        pos3 = e.clientX;
        pos4 = e.clientY;
        // set the element's new position:
        elmnt.style.top = (elmnt.offsetTop - pos2) + "px";
        elmnt.style.left = (elmnt.offsetLeft - pos1) + "px";
    }

    function closeDragElement() {
        // stop moving when mouse button is released:
        document.onmouseup = null;
        document.onmousemove = null;
    }
}
export default {
    data() {
        return {
            isOpened: true,
            isAnchored: true,
            isFullscreen: false,
        };
    },
    props: {
        title: {
            type: String,
            required: true,
        },
        allowDrag: {
            type: Boolean,
            default: false,
        },
        allowFullscreen: {
            type: Boolean,
            default: false,
        },
        allowClose: {
            type: Boolean,
            default: false,
        },
        allowCollapse: {
            type: Boolean,
            default: true,
        },

    },
    methods: {
        closePanelMethod(e) {
            this.$emit("closecurrentpanel");
        }
    },
    mounted() {
        dragElement(this.$refs.draggable, this.$refs.draggableHeader);
    }
}
</script>

<style lang="scss" scoped>
@import "@/static/css/form-styles.scss";

.fullscreen {
    position: fixed;
    width: 100%;
    height: 100vh;
    top: 0 !important;
    left: 0 !important;
    z-index: 1000;
    background-color: rgba($color: #000000, $alpha: 0.2);
    backdrop-filter: blur(1px);

    .header {
        padding: 0 20px;
    }

    .container {
        height: 90vh !important;
        margin: 0 5%;
    }

    .iframe {
        height: 80vh!important;
    }

}

.unanchored {
    position: fixed;
    max-width: 600px;
    top: 20vh;
    right: 20vw;
}

.container-outer {
    margin: 0;
    padding: 0;
    width: 100%;
    display: flex;
    align-items: center;
}

.anchored {}

.container {
    box-shadow: 0 2px 5px -2px var(--normalShadowColor);
    margin: 10px;
    border: 1px solid var(--interfaceSeparatorColor1);
    border-radius: 15px 15px 0px 0px;
    background-color: var(--interfaceBackgroundColor);
    max-height: 90vh;
    width: 100%;

    .header {
        display: flex;
        align-items: center;
        background-color: #fff;
        border-radius: 15px 15px 0px 0px;
        border-bottom: 1px solid var(--interfaceSeparatorColor1);
        height: 50px;
        cursor: pointer;
        transition: 0.2s;
        position: relative;

        .arrow-button {
            background: transparent;
            border: none;
            cursor: pointer;
        }

        button:focus {
            outline: none;
        }
    }

    .content {
        height: auto;
        height: 90%;
        max-height: 0;
        overflow: hidden;
        transition: max-height 0.15s ease-out;
        line-height: 1.7;
        margin: 0 28px;
    }

    .content-opened {
        padding: 10px;
        transition: max-height 0.15s ease-out;
        max-height: 1000px !important;
    }
}

.arrow-down {
    transform: rotate(90deg);
}

.arrow {
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 12px solid var(--interfaceItemsBorderColor);

    width: 0;
    height: 0;
    margin: 10px;
    transition: 0.3s;
    border-radius: 3px;
}

table {
    margin-left: 5px;
}

.buttons {
    background: auto;
    z-inder: 1000;
    position: absolute;
    right: 10px;
}

.draggable-header {
    width: 100%;
    height: 10px;
    padding: 20px 0;
}

.hidden {
    display: none;
}

h3 {
    white-space: nowrap;
}
</style>
