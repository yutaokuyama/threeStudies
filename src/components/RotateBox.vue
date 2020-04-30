<template>
  <div id="home">
    <canvas id="canvas" :width="canvasWidth" :height="canvasHeight"></canvas>
  </div>
</template>

<script>
import * as THREE from "three";
export default {
  name: "RotateBox",
  components: {},
  data() {
    const canvasWidth = window.innerWidth;
    const canvasHeight = window.innerHeight;
    const scene = new THREE.Scene();
    const renderer = null;
    const camera = new THREE.PerspectiveCamera(
      75,
      canvasWidth / canvasHeight,
      0.1,
      1000
    );
    const light = new THREE.DirectionalLight(0xffffff);
    const geometry = new THREE.BoxGeometry(400, 400, 400);
    const material = new THREE.MeshNormalMaterial();
    const cube = new THREE.Mesh(geometry, material);
    return {
      scene,
      renderer,
      camera,
      light,
      geometry,
      material,
      cube,
      canvasWidth,
      canvasHeight,
    };
  },
  methods: {
    handleResize: function() {
      this.canvasWidth = window.innerWidth;
      this.canvasHeight = window.innerHeight;
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(this.canvasWidth, this.canvasHeight);
      this.camera.aspect = this.canvasWidth / this.canvasHeight;
      this.camera.updateProjectionMatrix();
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.cube.rotation.x += 0.02;
      this.cube.rotation.z += 0.02;
      this.renderer.render(this.scene, this.camera);
    },
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);
    const _canvas = document.getElementById("canvas");
    this.renderer = new THREE.WebGLRenderer({
      antialias: true,
      canvas: _canvas
    });
    this.camera.position.set(0.0, 0.0, 800.0);
    this.light.position.set(0.0, 0.0, 10.0);
    this.scene.add(this.cube);
    this.animate();
  },
  beforeDestroy: function() {
    window.removeEventListener("resize", this.handleResize);
  }
};
</script>

<style scoped></style>
