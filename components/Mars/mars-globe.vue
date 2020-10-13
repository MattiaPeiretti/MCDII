<template>
  <div>
    <canvas style="width: 100%; height: 100%;" id="canvas"></canvas>
  </div>
</template>

<script>
import * as THREE from 'three';
import OrbitControls from './OrbitControls';

export default {
    async mounted() {

        const canvas = this.$el.querySelector('#canvas');

        const scene = new THREE.Scene();
			  const camera = new THREE.PerspectiveCamera( 30, canvas.clientWidth/ canvas.clientHeight, 0.1, 1000 );
        const renderer = new THREE.WebGLRenderer({ canvas });

        renderer.setSize(canvas.clientWidth, canvas.clientHeight, false);

        const controls = new OrbitControls(camera, renderer.domElement);
            
        controls.minDistance = 1.12; controls.maxDistance = 10;
        camera.position.z = 5;

        const loader = new THREE.TextureLoader();
        const map = loader.load(require('@/static/textures/2k_mars.jpg'));

        scene.add(new THREE.Mesh(new THREE.SphereBufferGeometry(1, 32, 32), new THREE.MeshBasicMaterial({map})));

        
        controls.addEventListener("change", () => renderer.render(scene, camera));
        renderer.render(scene, camera);
    }
}
</script>

<style scoped>

#canvas {
  cursor:move
}

</style>