<template>
<div>
  <div class="header">
    <h1>Query Console</h1>
    <span>Here you can prepare and submit a query to the Mars Climate Database.</span>
  </div>
  
  <div class="container-console">
    <div class="control-panel">
      <collapsable-panel title="Presets">wegroiuyegwborvybeoiutvb<br>ipè0943è0958jg0934g5jè09q3<br>wegroiuyegwborvybeoiutvb<br>ipè0943è0958jg0934g5jè09q3<br>wegroiuyegwborvybeoiutvb<br>ipè0943è0958jg0934g5jè09q3<br></collapsable-panel>
      <collapsable-panel title="Date Parameters"></collapsable-panel>
      <collapsable-panel title="Location Paramters"></collapsable-panel>
      <collapsable-panel title="Layers Selection"></collapsable-panel>
      <collapsable-panel title="Advanced Settings"></collapsable-panel>
      <collapsable-panel title="Graph Preferences"></collapsable-panel>

    </div>
    <div class="preview-panel">
    </div>
  </div>
</div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>

.container-console {
  padding-top: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 80%;
  margin: 0 auto;

}

.header {
  padding-top: 80px;
  width: 80%;
  margin: 0 auto;

  h1, span {
    padding: 10px;
  }
}

</style>
