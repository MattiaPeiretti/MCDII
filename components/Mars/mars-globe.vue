<template>
  <div>
    <canvas style="width: 100%; height: 100%;" id="canvas"></canvas>
  </div>
</template>

<script>
import * as THREE from 'three';

import { TrackballControls } from 'three/examples/jsm/controls/TrackballControls.js'

const loadTexture = () => {
        const loader = new THREE.TextureLoader();   
        return url => new Promise(resolve => loader.load(url, resolve));
        }

export default {
    async mounted() {
        const canvas = this.$el.querySelector('#canvas');
        var scene = new THREE.Scene();
			var camera = new THREE.PerspectiveCamera( 75, canvas.clientWidth/ canvas.clientHeight, 0.1, 1000 );
            

            var renderer = new THREE.WebGLRenderer({ canvas });
            renderer.setSize(canvas.clientWidth, canvas.clientHeight, false);
			// renderer.setSize( this.$el.innerWidth, this.$el.innerHeight );
			// this.$el.appendChild( renderer.domElement );

            const controls = new THREE.OrbitControls(camera, renderer.domElement);
            controls.minDistance = 1.12; controls.maxDistance = 10;

            camera.position.z = 5;


			// var animate = function () {
			// 	requestAnimationFrame( animate );

			// 	cube.rotation.x += 0.01;
			// 	cube.rotation.y += 0.01;

			// 	renderer.render( scene, camera );
			// };

            // animate();

            const map = await loadTexture(`https://solartextures.b-cdn.net/2k_mars.jpg`);
            scene.add(new THREE.Mesh(new THREE.SphereBufferGeometry(1, 32, 32), new THREE.MeshBasicMaterial({map})));

            renderer.render(scene, camera);
            controls.addEventListener("change", () => renderer.render(scene, camera));
            invalidation.then(() => (controls.dispose(), renderer.dispose()));

                    

    }
}
</script>
