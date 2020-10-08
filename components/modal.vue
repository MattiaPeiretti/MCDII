<template>
  <div>
    <div class="modal-container">
      <div class="modal-inner">
        <img
          class="close-modal-button"
          @click="closeModal()"
          src="@/static/icons/close-24px.svg"
          alt="delete"
        />
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    closeModal(e) {
      this.$emit("closeModal");
    },
  },
};
</script>

<style lang="scss" scoped>
.modal-container {
  background-color: rgba($color: #000000, $alpha: 0.2);
  backdrop-filter: blur(1px);
  border-radius: var(--interfaceBorderRadius);

  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100px;
  height: 100%;

  z-index: 99999;

  .modal-inner {
    position: relative;
    background-color: var(--interfaceBackgroundColor);
    width: 80%;
    box-shadow: 0 2px 5px -2px var(--normalShadowColor);
    border-radius: var(--interfaceBorderRadius);
    padding: 30px;
  }
}

.close-modal-button {
  position: absolute;
  top: 15px;
  right: 15px;
  cursor: pointer;

  &:hover {
    background-color: var(--interfaceSecondaryHoverColor);
    border-radius: 50px;
    transition: 0.5s;
  }
}
</style>