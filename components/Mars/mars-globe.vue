<template>
  <div>
    <canvas style="width: 100%; height: 100%;" id="canvas"></canvas>
  </div>
</template>

<script>
import * as THREE from "three";
import OrbitControls from "./OrbitControls";

export default {
  async mounted() {
    const loader = new THREE.TextureLoader();
    const map = await loader.load(
      require("@/static/textures/2k_mars.jpg"),
      () => {
        renderer.render(scene, camera);
      }
    );
    const canvas = this.$el.querySelector("#canvas");
    const w = canvas.clientWidth / 1.5,
      h = canvas.clientHeight / 1.5;
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      30,
      canvas.clientWidth / canvas.clientHeight,
      0.1,
      1000
    ).translateZ(5);

    const renderer = new THREE.WebGLRenderer({ canvas });

    renderer.setSize(canvas.clientWidth, canvas.clientHeight, false);

    // let globe = new THREE.Mesh(new THREE.SphereBufferGeometry(1, 32, 32), new THREE.MeshBasicMaterial({color: 0xffffff}));
    let globe = new THREE.Mesh(
      new THREE.SphereBufferGeometry(1, 32, 32),
      new THREE.MeshBasicMaterial({ map })
    );

    scene.add(globe);

    renderer.render(scene, camera);

    const controls = new OrbitControls(camera, renderer.domElement);

    controls.minDistance = 1.12;
    controls.maxDistance = 10;

    controls.update();

    controls.addEventListener("change", () => renderer.render(scene, camera));
    renderer.render(scene, camera);
  }
};
</script>

<style scoped>
#canvas {
  cursor: move;
}
</style>
