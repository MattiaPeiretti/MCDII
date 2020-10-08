<template>
  <div class="toolbar-container">
    <div class="preset-button-container" @click="openModalPresets">
      <div class="preset-button-container-inner">
        <img src="@/static/icons/analytics-24px.svg" alt="" />
        <span class="preset-button-title">Presets</span>
      </div>
    </div>
    <div class="preset-button-container">
      <div class="preset-button-container-inner">
        <img src="@/static/icons/analytics-24px.svg" alt="" />
        <span class="preset-button-title">Saved</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    openModalPresets(e) {
      this.$emit("openModalPresets");
    },
  },
};
</script>

<style lang="scss" scoped>
.toolbar-container {
  position: fixed;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
}

.preset-button-container {
  display: inline-block;
  padding: 5px;
  padding-right: 10px;
  margin-top: 10px;
  border: 1px solid var(--interfaceSeparatorColor1);
  background-color: var(--interfaceHeaderBackgroundColor);
  border-left: none !important;
  border-radius: 0 50% 50% 0;
  box-shadow: 0 2px 5px -2px var(--normalShadowColor);

  &:hover {
    border: 1px solid var(--interfaceActiveColor);

    cursor: pointer;
  }
}

.preset-button-container-inner {
  display: flex;
  flex-direction: column;
  min-width: 50px;
  height: 50px;
  text-align: center;
  align-items: center;
  justify-content: center;

  img {
    fill: red !important;
  }
}
</style>