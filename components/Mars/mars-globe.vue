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
    ).translateZ(50);

    const renderer = new THREE.WebGLRenderer({ canvas });

    const raycaster = new THREE.Raycaster();
    let mouse = new THREE.Vector2();

    renderer.setSize(canvas.clientWidth, canvas.clientHeight, false);

    // let globe = new THREE.Mesh(new THREE.SphereBufferGeometry(1, 32, 32), new THREE.MeshBasicMaterial({color: 0xffffff}));
    let globe = new THREE.Mesh(
      new THREE.SphereBufferGeometry(2, 32, 32),
      new THREE.MeshBasicMaterial({ map })
    );

    let pointer = new THREE.Mesh(
      new THREE.SphereBufferGeometry(0.1, 32, 32),
      new THREE.MeshBasicMaterial({ color: 0xffffff })
    );

    scene.add(globe);
    scene.add(pointer);

    pointer.position.set(0, 0, 0);
    globe.position.set(0, 0, 0);

    const controls = new OrbitControls(camera, renderer.domElement);

    controls.minDistance = 1.12;
    controls.maxDistance = 10;
    controls.enablePan = false;

    controls.update();

    controls.addEventListener("change", () => renderer.render(scene, camera));

    function onMouseMove( event ) {
      
      if (event.button == 0) return;
      event.preventDefault();
      // calculate mouse position in normalized device coordinates
      // (-1 to +1) for both components
      let canvasBounds = renderer.context.canvas.getBoundingClientRect();
      mouse.x = ( ( event.clientX - canvasBounds.left ) / ( canvasBounds.right - canvasBounds.left ) ) * 2 - 1;
      mouse.y = - ( ( event.clientY - canvasBounds.top ) / ( canvasBounds.bottom - canvasBounds.top) ) * 2 + 1;
      render();
    }

    function render() {

      // update the picking ray with the camera and mouse position
      raycaster.setFromCamera( mouse, camera );

      // calculate objects intersecting the picking ray
      var intersects = raycaster.intersectObjects( scene.children, true);
      console.log(intersects);
      for ( var i = 0; i < intersects.length; i++ ) {
        
        pointer.position.set(intersects[ i ].point.x, intersects[ i ].point.y, intersects[ i ].point.z);

      }

      renderer.render( scene, camera );

    }

    canvas.addEventListener( 'mousedown', onMouseMove, false );

  }
};
</script>

<style scoped>
#canvas {
  cursor: move;
}
</style>
