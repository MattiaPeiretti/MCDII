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
        <collapsable-panel title="Date Parameters">
          <p class="panel-title"><b>Mars Date:</b></p>
          <p>
            Solar longitude (Ls):
            <input class="number-input-textbox" type="text" /> degrees
          </p>
          <p>
            Local Time:
            <input class="number-input-textbox" type="text" /> Matian hour
          </p>
          <p class="panel-title"><b>Earth Date:</b></p>
          <p>Date:</p>
          <client-only
            ><date-picker
              placeholder="MM/DD/YYYY"
              format="MM/dd/yyyy"
              v-model="date_today"
          /></client-only>
          <p>Time:</p>
          <input
            type="text"
            :placeholder="
              currentDate.getHours() +
                ':' +
                currentDate.getMinutes() +
                ':' +
                currentDate.getSeconds()
            "
          />
        </collapsable-panel>
        <collapsable-panel title="Location Paramters">
          <p class="panel-title"><b>Coordinates on Mars</b></p>
          <p>
            Latitude: <input class="number-input-textbox" type="text" /> degree
            North
          </p>
          <p>
            Longitude: <input class="number-input-textbox" type="text" /> degree
            East
          </p>
          <p>
            Altitude: <input class="number-input-textbox" type="text" />
            <select>
              <option>meters above surface</option>
              <option>meters above sea level</option>
              <option>meters from Mars center</option>
              <option>Pa (pressure level)</option>
            </select>
          </p>
        </collapsable-panel>
        <collapsable-panel title="Layers Selection">
        <layer-editor></layer-editor>
        </collapsable-panel>
        <collapsable-panel title="Advanced Settings">
          <p class="panel-title"><b>Customize Data Request:</b></p>
          <ul>
            <li>
              <input
                type="checkbox"
                id="same-local-time"
                name="same-local-time"
                value=""
              />
              <lable for="same-local-time"
                >Same <i>local time</i> on range of longitudes</lable
              >
            </li>
            <li>
              <input
                type="checkbox"
                id="high-reslolution"
                name="high-reslolution"
                value=""
              />
              <lable for="high-reslolution"
                >Use <i>high resolution topography</i></lable
              >
            </li>
            <li>
              <input
                type="checkbox"
                id="zonal-averaging"
                name="zonal-averaging"
                value=""
              />
              <lable for="same-local-time"
                >Zonal averaging (only lat/alt plot)</lable
              >
            </li>
            <li>
              <i>Dust/EUV scenario</i>
              <select name="dust-euv-scenario">
                <option value="1" selected="">climatology ave solar</option>
                <option value="2">climatology min solar</option>
                <option value="3">climatology max solar</option>
                <option value="4">dust storm min solar</option>
                <option value="5">dust storm ave solar</option>
                <option value="6">dust storm max solar</option>
                <option value="7">warm (dusty, max solar)</option>
                <option value="8">cold (low dust, min solar)</option>
                <option value="24">Martian Year 24 </option>
                <option value="25">Martian Year 25 </option>
                <option value="26">Martian Year 26 </option>
                <option value="27">Martian Year 27 </option>
                <option value="28">Martian Year 28 </option>
                <option value="29">Martian Year 29 </option>
                <option value="30">Martian Year 30 </option>
                <option value="31">Martian Year 31 </option>
                <option value="32">Martian Year 32 </option>
                <option value="33">Martian Year 33 </option>
              </select>
            </li>
          </ul>
        </collapsable-panel>
        <collapsable-panel title="Graph Preferences">
          <ul>
            <li>
              Figure format
              <input type="radio" name="dpi" value="80" checked="" /> PNG
              <input type="radio" name="dpi" value="160" /> PNG hi-res
              <input type="radio" name="dpi" value="eps" /> EPS
            </li>
            <li>
              [1D] Log(values)
              <input type="radio" name="islog" value="off" checked="" /> off
              <input type="radio" name="islog" value="on" /> on
            </li>
            <li>
              [2D] Colormap
              <select name="colorm">
                <option value="jet" selected="">blue green yellow red</option>
                <option value="Greys">grey</option>
                <option value="Blues">blue</option>
                <option value="YlOrRd">yellow orange red</option>
                <option value="spectral">rainbow</option>
                <option value="hot">black red yellow</option>
                <option value="RdBu_r">blue white red</option>
                <option value="RdBu">red white blue</option>
              </select>
            </li>
            <li>
              [2D] Values range <input type="text" size="2" name="minval" /> to
              <input type="text" size="2" name="maxval" />
            </li>
            <li>
              [2D map]
              <select name="proj">
                <!--<option value=""          selected>flat (cylindrical lat-lon)</option>-->
                <option value="cyl" selected="">flat</option>
                <option value="ortho">sphere</option>
                <option value="npstere">N pole</option>
                <option value="spstere">S pole</option>
                <!--<option value="robin">map</option>-->
                <!--<option value="laea">laea</option>-->
              </select>
              proj @ lat <input type="text" size="1" name="plat" /> lon
              <input type="text" size="1" name="plon" />
            </li>
            <li>
              [2D map] Transparency (%)
              <input type="text" size="1" name="trans" />
            </li>
            <li>
              [2D map] Wind vectors
              <input type="radio" name="iswind" value="off" checked="" /> off
              <input type="radio" name="iswind" value="on" /> on
            </li>

            <li>
              [2D map]
              <input type="checkbox" name="istherepoint" value="on" /> Point at
              lat <input type="text" size="1" name="latpoint" /> lon
              <input type="text" size="1" name="lonpoint" />
            </li>
          </ul>
        </collapsable-panel>
      </div>
      <div class="preview-panel"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: new Date()
    };
  }
};
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
