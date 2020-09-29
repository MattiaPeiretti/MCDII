<template>
  <div>
    <nav-desktop v-if="!mobileView" />
    <nav-mobile v-if="mobileView" />
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      mobileView: true,
    };
  },
  methods: {
    handleView() {
      this.mobileView = window.innerWidth <= 790;
    },
  },
  created() {
    this.handleView();
    window.addEventListener("resize", this.handleView);
  },
};
</script>