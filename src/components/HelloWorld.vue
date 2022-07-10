<template>
  <div class="hello"></div>
</template>

<script>
import * as Three from "three";
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
import TrackballControls from "three-trackballcontrols";

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
    methods: {

      function () {
      const loader = new GLTFLoader();
      loader.load( 'path/to/model.glb', function ( gltf ) {
      scene.add( gltf.scene );
      }, undefined, function ( error ) {
      console.error( error );
      } );
      },

    init: function () {
      let container = document.getElementById("container");

      console.log(TrackballControls);

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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
