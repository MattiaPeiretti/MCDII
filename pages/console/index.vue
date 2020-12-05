<template>
<div class="main-container">
    <toolbar @openModalPresets="isPresetsModalOpened = true"></toolbar>

    <div class="header">
        <h1>Query Console</h1>
        <span>Here you can prepare and submit a query to the Mars Climate
            Database.</span>
    </div>

    <div class="container-console">
        <div class="control-panel">
            <collapsable-panel title="Date Parameters" v-bind:showWindowControls="false">
                <p class="panel-title"><b>Mars Date:</b></p>

                <table>
                    <tr>
                        <td><info-text v-on:clicked="updateCurrentInfoUrl('http://www-mars.lmd.jussieu.fr/mars/time/solar_longitude.html')">Solar longitude</info-text>(Ls):</td>
                        <td>
                            <input class="number-input-textbox" type="text" /> degrees
                        </td>
                        <td class="use-all-td">
                            <input type="checkbox" name="all-solar-longitude" value="" />
                            <label for="all-solar-longitude">All</label>
                        </td>
                    </tr>
                    <tr>
                        <td><info-text v-on:clicked="updateCurrentInfoUrl('http://www-mars.lmd.jussieu.fr/mars/time/local_time.html')">Local Time:</info-text></td>
                        <td>
                            <input class="number-input-textbox" type="text" /> Matian hour
                        </td>
                        <td class="use-all-td">
                            <input type="checkbox" name="all-solar-longitude" value="" />
                            <label for="all-solar-longitude">All</label>
                        </td>
                    </tr>
                </table>

                <p class="panel-title"><b>Earth Date:</b></p>
                <p>Date:</p>
                <client-only>
                    <date-picker placeholder="MM/DD/YYYY" format="MM/dd/yyyy" v-model="currentDate" />
                </client-only>
                <p>Time:</p>
                <input type="text" :placeholder="
              currentDate.getHours() +
                ':' +
                currentDate.getMinutes() +
                ':' +
                currentDate.getSeconds()
            " />
            </collapsable-panel>

            <collapsable-panel title="Location Paramters" v-bind:showWindowControls="false">
                <p class="panel-title"><b>Coordinates on Mars</b></p>

                <table>
                    <tr>
                        <td>Latitude:</td>
                        <td>
                            <input class="number-input-textbox" type="text" /> degree North
                        </td>
                        <td class="use-all-td">
                            <input type="checkbox" name="all-solar-longitude" value="" />
                            <label for="all-solar-longitude">All</label>
                        </td>
                    </tr>
                    <tr>
                        <td>Longitude:</td>
                        <td>
                            <input class="number-input-textbox" type="text" /> degree East
                        </td>
                        <td class="use-all-td">
                            <input type="checkbox" name="all-solar-longitude" value="" />
                            <label for="all-solar-longitude">All</label>
                        </td>
                    </tr>
                    <tr>
                        <td>Altitude:</td>
                        <td>
                            <input class="number-input-textbox" type="text" />
                            <select>
                                <option>meters above surface</option>
                                <option>meters above sea level</option>
                                <option>meters from Mars center</option>
                                <option>Pa (pressure level)</option>
                            </select>
                        </td>
                        <td class="use-all-td">
                            <input type="checkbox" name="all-solar-longitude" value="" />
                            <label for="all-solar-longitude">All</label>
                        </td>
                    </tr>
                </table>
            </collapsable-panel>

            <collapsable-panel title="Layers Selection" v-bind:showWindowControls="false">
                <layer-editor></layer-editor>
            </collapsable-panel>

            <collapsable-panel title="Advanced Settings" v-bind:showWindowControls="false">
                <p class="panel-title"><b>Customize Data Request:</b></p>
                <table>
                    <tr>
                        <td>
                            <input type="checkbox" id="same-local-time" name="same-local-time" value="" />
                            <label for="same-local-time">Same <info-text v-on:clicked="updateCurrentInfoUrl('http://www-mars.lmd.jussieu.fr/mars/time/local_time.html')">local time</info-text> on range of longitudes</label>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <input type="checkbox" id="high-reslolution" name="high-reslolution" value="" />
                            <label for="high-reslolution">Use <info-text v-on:clicked="updateCurrentInfoUrl('http://www-mars.lmd.jussieu.fr/mars/info_web/index.html#highres')">high resolution topography</info-text></label>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <input type="checkbox" id="zonal-averaging" name="zonal-averaging" value="" />
                            <label for="same-local-time">Zonal averaging (only lat/alt plot)</label>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <info-text v-on:clicked="updateCurrentInfoUrl('http://www-mars.lmd.jussieu.fr/mars/info_web/index.html#scenarios')">Dust/EUV scenario</info-text>
                            <select name="dust-euv-scenario">
                                <option value="1" selected="">climatology ave solar</option>
                                <option value="2">climatology min solar</option>
                                <option value="3">climatology max solar</option>
                                <option value="4">dust storm min solar</option>
                                <option value="5">dust storm ave solar</option>
                                <option value="6">dust storm max solar</option>
                                <option value="7">warm (dusty, max solar)</option>
                                <option value="8">cold (low dust, min solar)</option>
                                <option value="24">Martian Year 24</option>
                                <option value="25">Martian Year 25</option>
                                <option value="26">Martian Year 26</option>
                                <option value="27">Martian Year 27</option>
                                <option value="28">Martian Year 28</option>
                                <option value="29">Martian Year 29</option>
                                <option value="30">Martian Year 30</option>
                                <option value="31">Martian Year 31</option>
                                <option value="32">Martian Year 32</option>
                                <option value="33">Martian Year 33</option>
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td></td>
                    </tr>
                </table>
            </collapsable-panel>

            <collapsable-panel title="Graph Preferences" :allowDrag="true" :allowFullscreen="true" v-bind:showWindowControls="true">
                <p class="panel-title"><b>General:</b></p>
                <table>
                    <tr>
                        <td>Figure Format</td>
                        <td>
                            <select name="" id="">
                                <option value="80">PNG</option>
                                <option value="160">PNG HiRes</option>
                                <option value="eps">EPS</option>
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>Log values (1D)</td>
                        <td>
                            <input type="checkbox" name="istherepoint" value="on" /> Active
                        </td>
                    </tr>
                </table>

                <p class="panel-title"><b>2D settings:</b></p>

                <table>
                    <tr>
                        <td>Colormap</td>
                        <td>
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
                        </td>
                    </tr>
                    <tr>
                        <td>Values range</td>
                        <td>
                            <input type="text" size="2" name="minval" /> to
                            <input type="text" size="2" name="maxval" />
                        </td>
                    </tr>
                </table>

                <p class="panel-title"><b>2D map settings:</b></p>
                <table>
                    <tr>
                        <td>Map type:</td>
                        <td>
                            <select name="proj">
                                <!--<option value=""          selected>flat (cylindrical lat-lon)</option>-->
                                <option value="cyl" selected="">flat</option>
                                <option value="ortho">sphere</option>
                                <option value="npstere">N pole</option>
                                <option value="spstere">S pole</option>
                                <!--<option value="robin">map</option>-->
                                <!--<option value="laea">laea</option>-->
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>Project at</td>
                        <td>
                            latitude <input type="text" size="1" name="plat" /> longitude
                            <input type="text" size="1" name="plon" />
                        </td>
                    </tr>
                    <tr>
                        <td>Transparency:</td>
                        <td><input type="text" size="1" name="trans" /></td>
                    </tr>
                    <tr>
                        <td>Wind vectors</td>
                        <td>
                            <input type="checkbox" name="istherepoint" value="on" /> Active
                        </td>
                    </tr>
                    <tr>
                        <td>Point at specific coordinates</td>
                        <td>
                            <input type="checkbox" name="istherepoint" value="on" />Active
                            at latitude
                            <input type="text" size="1" name="latpoint" /> longitude
                            <input type="text" size="1" name="lonpoint" />
                        </td>
                    </tr>
                </table>
            </collapsable-panel>

            
        </div>
        <div class="preview-panel">
            <collapsable-panel title="3D Overview" :allowDrag="true" :allowFullscreen="true" v-bind:showWindowControls="true">
                <mars-globe></mars-globe>
            </collapsable-panel>
        </div>
    </div>

    <div class="modals">
        <modal v-if="isPresetsModalOpened" @closeModal="isPresetsModalOpened = false">
            <p class="panel-title"><b>Rovers / Landers: </b></p>
            <preset-button>Not At Equator</preset-button>
            <preset-button>InSight</preset-button>
            <preset-button>Curiosity</preset-button>
            <preset-button>Phoenix</preset-button>
            <preset-button>Oppoirtunity</preset-button>
            <preset-button>Spirit</preset-button>
            <preset-button>Pathfinder</preset-button>
            <preset-button>Viking 1</preset-button>
            <preset-button>Viking 2</preset-button>

            <p class="panel-title"><b>Time of the day: </b></p>
            <preset-button>Morning</preset-button>
            <preset-button>Afternoon</preset-button>
            <preset-button>Evening</preset-button>
            <preset-button>Night</preset-button>

            <p class="panel-title"><b>Altitude: </b></p>
            <preset-button>Near Surface</preset-button>
            <preset-button>Boundary Layer</preset-button>
            <preset-button>Troposhpere</preset-button>
            <preset-button>Mesosphere</preset-button>
            <preset-button>Thermosphere</preset-button>

            <p class="panel-title"><b>Interst: </b></p>
            <preset-button>Atmosphere</preset-button>
            <preset-button>Winds</preset-button>
            <preset-button>Weather</preset-button>
            <preset-button>Water Cycle</preset-button>
            <preset-button>Chemistry</preset-button>
            <preset-button>Landing Engeneereing</preset-button>
            <preset-button>Glaciology</preset-button>
            <preset-button>Surface Meteorology</preset-button>
            <preset-button>Radiative Balance</preset-button>
        </modal>
    </div>
    <div class="dock">
        <info-iframe :class="{'hidden':!showInfoPanel}" ref="infoFrame" :currentURL="currentInfoUrl" v-on:closecurrentpanel="closeInfoPanel()"></info-iframe>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            currentDate: new Date(),
            isPresetsModalOpened: false,
            currentInfoUrl: "",
            showInfoPanel: false,
        };
    },
    methods: {
        updateCurrentInfoUrl(url) {
            this.currentInfoUrl = url;
            this.showInfoPanel = true;

            
        },
        closeInfoPanel(e) {
            this.showInfoPanel = false;
        }
    },

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

.dock {
    position: fixed;
    bottom: 30px;
    right: 0;
    min-width: 500px;
    z-index: 999;
}

.hidden {
    display: none;
    pointer-events: none;
}

html, body {
  height: 100%;
}
</style>
