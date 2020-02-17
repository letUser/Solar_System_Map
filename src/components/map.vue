<template>
  <div class="map"></div>
</template>

<script>
import * as THREE from "three";

const renderer = new THREE.WebGLRenderer({ alpha: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

let camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
camera.position.set(0, 0, 100);
camera.lookAt(0, 0, 0);

const scene = new THREE.Scene();
const loader = new THREE.TextureLoader();

const geometry = new THREE.SphereGeometry(1, 22, 23);
const material = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://img1.goodfon.ru/wallpaper/nbig/b/50/poligony-linii-grani-solnce.jpg"
  )
});
const sun = new THREE.Mesh(geometry, material);
scene.add(sun);

camera.position.z = 15;

const animate = function() {
  requestAnimationFrame(animate);

  sun.rotation.y += 0.001;

  renderer.render(scene, camera);
};

animate();

export default {
  name: "Map",
  props: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>