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

      this.camera = new Three.PerspectiveCamera(
        75,
        container.clientWidth / container.clientHeight,
        0.01,
        10
      );
      this.camera.position.z = 1;

      this.scene = new Three.Scene();

      let Loader = new GLTFLoader();
      Loader.load('../don2-6-forVSC.gltf', function (gltf) {
      this.scene.add(gltf.scene);
      });
    },

  },
  mounted() {
    this.init();
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