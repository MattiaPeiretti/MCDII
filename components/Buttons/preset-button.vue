<template>
  <div class="preset-button-container">
    <div class="preset-button-container-inner">
      <img src="@/static/icons/analytics-24px.svg" alt="" />
      <span class="preset-button-title"><slot></slot></span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.preset-button-container {
  display: inline-block;
  padding: 5px;
  border: 1px solid var(--interfaceItemsBorderColor);

  border-radius: var(--interfaceBorderRadius);
  margin: 5px;

  &:hover {
    border: 1px solid var(--interfaceActiveColor);
    box-shadow: 0 2px 5px -2px var(--normalShadowColor);
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
}
</style>