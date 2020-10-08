<template>
  <div class="container">
    <div class="header" @click="isOpened = !isOpened">
      <div
        class="arrow"
        :class="{
          'arrow-down': isOpened,
        }"
      ></div>
      <h3>{{ title }}</h3>
    </div>

    <div
      class="content"
      :class="{
        'content-opened': isOpened,
      }"
    >
      <slot></slot>
    </div>
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
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/static/css/form-styles.scss";

.container {
  box-shadow: 0 2px 5px -2px var(--normalShadowColor);
  margin: 10px;
  border: 1px solid var(--interfaceSeparatorColor1);
  border-radius: 15px 15px 0px 0px;
  background-color: var(--interfaceBackgroundColor);

  .header {
    display: flex;
    align-items: center;
    background-color: #fff;
    border-radius: 15px 15px 0px 0px;
    border-bottom: 1px solid var(--interfaceSeparatorColor1);
    height: 50px;
    cursor: pointer;
    transition: 0.2s;

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
    height: auto;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.15s ease-out;
    line-height: 1.7;
  }

  .content-opened {
    padding: 10px;
    transition: max-height 0.15s ease-out;
    max-height: 500px !important;
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
</style>
