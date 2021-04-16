<template> </template>
<script>
import * as THREE from "three";
import { OrbitControls } from "../../../../examples/jsm/controls/OrbitControls";
import { GLTFLoader } from "../../../../examples/jsm/loaders/GLTFLoader";
export default {
  name: "ProductView",
  data() {
    return {
      scene: undefined,
      camera: undefined,
      renderer: undefined
    };
  },
  props: {
    containerId: {
      type: String,
      required: true
    },
    modelSettings: {
      type: Object,
      required: true
    }
  },
  methods: {
    init() {
      this.scene = new THREE.Scene();
      this.scene.background = null;

      this.renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.toneMapping = THREE.ACESFilmicToneMapping;
      this.renderer.toneMappingExposure = 1;
      this.renderer.outputEncoding = THREE.sRGBEncoding;
      const container = document.getElementById(this.containerId);
      this.renderer.setSize(container.offsetWidth, container.offsetHeight);
      container.appendChild(this.renderer.domElement);

      // START: Adding camera
      this.camera = new THREE.PerspectiveCamera(
        45,
        container.offsetWidth / container.offsetHeight,
        0.25,
        20
      );
      this.camera.position.set(this.modelSettings.cameraPosition[0], this.modelSettings.cameraPosition[1], this.modelSettings.cameraPosition[2]);
      // END: Adding camera

      // START: Adding controls
      const controls = new OrbitControls(this.camera, this.renderer.domElement);

      controls.minDistance = 2;
      controls.maxDistance = 5;
      // controls.enablePan = false;
      controls.target.set(0, 0, 0);
      controls.addEventListener("change", this.renderScene); // use if there is no animation loop
      // END: Adding controls

      // START: Adding light
      const hlight = new THREE.AmbientLight(0x0f0f0f, 30);
      this.scene.add(hlight);

      const directionalLight = new THREE.DirectionalLight(0xffffff, 2);
      directionalLight.position.set(0, 1, 0);
      directionalLight.castShadow = true;
      this.scene.add(directionalLight);
      const light = new THREE.PointLight(0xffffcc, 1);
      light.position.set(0, 600, 1000);
      this.scene.add(light);
      const light2 = new THREE.PointLight(0xe6f7ff, 1);
      light2.position.set(1000, 200, 0);
      this.scene.add(light2);
      const light3 = new THREE.PointLight(0xfff2e6, 1);
      light3.position.set(0, 200, -1000);
      this.scene.add(light3);
      const light4 = new THREE.PointLight(0xc4c400, 1);
      light4.position.set(-1000, 600, 1000);
      this.scene.add(light4);
      // END: Adding light

      // START: Adding gtlf model
      let loader = new GLTFLoader();
      loader.load(
        this.modelSettings.link,
        data => {
          var object = data.scene;
          object.position.set(0,0,0);
          if(this.modelSettings.scale) object.scale.set(this.modelSettings.scale, this.modelSettings.scale, this.modelSettings.scale);
          this.scene.add(object);
          this.renderScene();
        }
      );
      // END: Adding gtlf model
    },
    renderScene() {
      this.renderer.render(this.scene, this.camera);
    }
  },
  mounted() {
    this.init();
    this.renderScene();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
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
