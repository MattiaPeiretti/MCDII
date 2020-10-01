<template>
  <div class="main-container">
    <div class="header">
      <h1>Query Console</h1>
      <span
        >Here you can prepare and submit a query to the Mars Climate
        Database.</span
      >
    </div>

    <div class="container-console">
      <div class="control-panel">
        <collapsable-panel title="Presets">
          <p><input type="text" /></p>
          <p><button>This is a test button</button></p>
          <p>
            <input type="radio" name="picked" value="one" />
            <input type="radio" name="picked" value="two" />
          </p>
          <p>
            <input type="checkbox" id="vehicle1" name="vehicle1" value="Bike" />
            <lable for="vehicle1">This is a test</lable>
          </p>
          <p>
            <select v-model="selected">
              <option>one</option>
              <option>two</option>
            </select>
          </p>
        </collapsable-panel>
        <collapsable-panel title="Date Parameters"></collapsable-panel>
        <collapsable-panel title="Location Paramters"></collapsable-panel>
        <collapsable-panel title="Layers Selection"></collapsable-panel>
        <collapsable-panel title="Advanced Settings"></collapsable-panel>
        <collapsable-panel title="Graph Preferences"></collapsable-panel>
      </div>
      <div class="preview-panel"></div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.main-container {
  color: var(--consoleForegroundColor);
  background-color: var(--consoleBackgroundColor);
  min-height: 100vh;
}

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

  h1,
  span {
    padding: 10px;
  }
}
</style>
