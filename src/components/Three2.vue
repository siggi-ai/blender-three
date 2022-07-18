<template>
  <div id="container"></div>
</template>

<script>
import * as Three from "three";
import GLTFLoader from 'three-gltf-loader';

export default {
  name: "ThreeTest",
  /* data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null,
    };
  }, */
  methods: {
    init: function () {
      let container = document.getElementById("container");

      console.log(GLTFLoader);

      this.camera = new Three.PerspectiveCamera(
        75,
        container.clientWidth / container.clientHeight,
        0.01,
        10
      );
      this.camera.position.z = 1;

      this.scene = new Three.Scene();

      let geometry = new Three.BoxGeometry(0.2, 0.2, 0.2);
      let material = new Three.MeshNormalMaterial();

      this.mesh = new Three.Mesh(geometry, material);
      this.scene.add(this.mesh);
/* 
      let Loader = new GLTFLoader();
      Loader.load('../don2-6-forVSC.gltf', function (gltf) {
      this.scene.add(gltf.scene);
      }); */

      this.renderer = new Three.WebGLRenderer({ antialias: true, alpha: true });
      this.renderer.setSize(container.clientWidth, container.clientHeight);
      container.appendChild(this.renderer.domElement);
    },
    animate: function () {
      requestAnimationFrame(this.animate);
      this.mesh.rotation.x += 0.01;
      this.mesh.rotation.y += 0.01;
      this.renderer.render(this.scene, this.camera);
    },
  },
  mounted() {
    this.init();
    this.animate();
  },
};
</script>

<style scoped>
#container {
  width: 800px;
  height: 800px;
  margin: 0 auto;
  margin-top: -200px;
}
</style>