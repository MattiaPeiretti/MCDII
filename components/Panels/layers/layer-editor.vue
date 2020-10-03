<template>
  <div class="layer-editor-container">
    <div class="controls">
      <button @click="isModalOpened = !isModalOpened">Add New Layer</button>
      <button @click="clearAllLayers()">Clear All</button>
    </div>
    <layer-crumb v-for="crumb in layers" :data="crumb" @deleteCrumb="removeLayer(crumb.id)"></layer-crumb>
    <p v-if="maxLayersAmountReached">You cant add any more layers!</p>
    <div v-if="isModalOpened" class="layer-editor-modal">
      <div class="layer-editor-modal-inner">
        <p v-if="maxLayersAmountReached">You cant add any more layers!</p>
        <p>
          Choose layer type:
          <select v-model="layerTypeSelect">
            <option v-for="layerType in layerTypes" v-bind:value="{ id: layerType.id, text: layerType.text }">{{ layerType.text }}</option>
          </select>
          <br />
        </p>
        <button @click="isModalOpened = false">Cancel</button>
        <button @click="addLayer(layerTypeSelect.id, layerTypeSelect.text)">Create</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isModalOpened: false,
      layers: [],
      maxLayersAmountReached: false,
      layerTypeSelect: '',
      layerTypes: [
          {id: 't', text: 'Temperature (K)'},
          {id: 'p', text: 'Pressure (Pa)'},
          {id: 'rho', text: 'Density (kg/m3)'},
          {id: 'wind', text: 'Horizontal wind (m/s)'},
          {id: 'w', text: 'Vertical wind (m/s, pos. when downward)'},
          {id: 'u', text: 'W-E wind component (m/s)'},
          {id: 'v', text: 'S-N wind component (m/s)'},
          {id: 'tsurf', text: 'Surface '},
          {id: 'ps', text: 'Surface pressure (Pa)'},
          {id: 'tau', text: 'Dust column vis opt depth above surf'},
          {id: 'qdust', text: 'Dust mass mixing ratio (kg/kg)'},
          {id: 'rdust', text: 'Dust effective radius (m)'},
          {id: 'sdust', text: 'Dust deposition on flat surface (kg/m2/s)'},
          {id: 'mtot', text: 'Water vapor column (kg/m2)'},
          {id: 'icetot', text: 'Water cloud ice column (kg/m2)'},
          {id: 'h2ovap', text: 'Water vapor vol. mixing ratio (mol/mol)'},
          {id: 'h2oice', text: 'Water ice mixing ratio (mol/mol)'},
          {id: 'rice', text: 'Water ice effective radius (m)'},
          {id: 'co2ice', text: 'Surface CO2 ice layer (kg/m2)'},
          {id: 'groundice', text: 'Surface H2O ice layer (kg/m2, 0.5: perennial)'},
          {id: 'pbl', text: 'Convective PBL height (m)'},
          {id: 'stress', text: 'Surf. wind stress (Kg/m/s2)'},
          {id: 'updraft', text: 'Max PBL updraft wind (m/s)'},
          {id: 'downdraft', text: 'Max PBL downdraft wind (m/s)'},
          {id: 'pblwvar', text: 'PBL vert wind variance (m2/s2)'},
          {id: 'pblhvar', text: 'PBL eddy vert heat flux (m/s/K)'},
          {id: 'ps_ddv', text: 'Surf. pres. day to day variability (Pa)'},
          {id: 'p_ddv', text: 'Pressure day to day variability (Pa)'},
          {id: 't_ddv', text: 'Temperature day to day variability (K)'},
          {id: 'u_ddv', text: 'Zonal wind day to day variability (m/s)'},
          {id: 'v_ddv', text: 'Merid. wind day to day variability (m/s)'},
          {id: 'w_ddv', text: 'Vert. wind day to day variability (m/s)'},
          {id: 'rho_ddv', text: 'Density day to day variability (kg/m^3)'},
          {id: 'tau_ddv', text: 'Dust column day to day variability'},
          {id: 'tsurfmx', text: 'Daily max mean surf '},
          {id: 'tsurfmn', text: 'Daily min mean surf '},
          {id: 'lwdown', text: 'Thermal IR flux to surface (W/m2)'},
          {id: 'swdown', text: 'Solar flux to surface (W/m2)'},
          {id: 'lwup', text: 'Thermal IR flux to space (W/m2)'},
          {id: 'swup', text: 'Solar flux reflected to space (W/m2)'},
          {id: 'co2col', text: 'CO2 column (kg/m2)'},
          {id: 'arcol', text: 'Ar column (kg/m2)'},
          {id: 'n2col', text: 'N2 column (kg/m2)'},
          {id: 'cocol', text: 'CO column (kg/m2)'},
          {id: 'o3col', text: 'O3 column (kg/m2)'},
          {id: 'co2', text: '[CO2] vol. mixing ratio (mol/mol)'},
          {id: 'ar', text: '[Ar] vol. mixing ratio (mol/mol)'},
          {id: 'n2', text: '[N2] vol. mixing ratio (mol/mol)'},
          {id: 'co', text: '[CO] vol. mixing ratio (mol/mol)'},
          {id: 'o3', text: '[O3] ozone vol. mixing ratio (mol/mol)'},
          {id: 'o', text: '[O] vol. mixing ratio (mol/mol)'},
          {id: 'o2', text: '[O2] vol. mixing ratio (mol/mol)'},
          {id: 'hydro', text: '[H] vol. mixing ratio (mol/mol)'},
          {id: 'hydro2', text: '[H2] vol. mixing ratio (mol/mol)'},
          {id: 'e', text: 'Electron number density (cm-3)'},
          {id: 'ecol', text: 'Total Electronic Content (TEC) (m-2)'},
          {id: 'hecol', text: 'He column (kg/m2)'},
          {id: 'he', text: '[He] vol. mixing ratio (mol/mol)'},
          {id: 'cp', text: 'Air heat capacity Cp (J kg-1 K-1)'},
          {id: 'visc', text: 'Air viscosity estimation (N s m-2)'},
      ]
    };
  },
  methods: {
    addLayer(type, name) {
      if (this.layers.length > 3) {
        this.maxLayersAmountReached = true;
      } else {
        this.maxLayersAmountReached = false;
        this.layers.push({
          id: this.layers.length,
          name: name,
          type: type,
        });
      }
    },
    removeLayer(id) {
        this.layers.splice(id, 1);
        this.layers.forEach(layer => {
            layer.id = this.layers.indexOf(layer);
        })
    },
    clearAllLayers() {
      this.layers = [];
      this.maxLayersAmountReached = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.layer-editor-container {
  position: relative;
  width: 100%;
  min-height: 100px;
}

.layer-editor-modal {
  background-color: rgba($color: #000000, $alpha: 0.2);
  backdrop-filter: blur(1px);

  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100px;

  .layer-editor-modal-inner {
    background-color: var(--interfaceBackgroundColor);
    width: 80%;
    box-shadow: 0 2px 5px -2px var(--normalShadowColor);
    border-radius: var(--interfaceBorderRadius);
    padding: 10px;
  }
}
</style>
