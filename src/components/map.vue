<template>
  <div class="map"></div>
</template>

<script>
import * as THREE from "three";

const renderer = new THREE.WebGLRenderer({ alpha: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

let camera = new THREE.PerspectiveCamera(
  100,
  window.innerWidth / window.innerHeight,
  1,
  500
);
camera.position.set(0, 0, 100);
camera.lookAt(20, 0, 0);

const scene = new THREE.Scene();
const loader = new THREE.TextureLoader();

const sunGeometry = new THREE.SphereGeometry(3, 22, 23);
const sunMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://img1.goodfon.ru/wallpaper/nbig/b/50/poligony-linii-grani-solnce.jpg"
  )
});
const sun = new THREE.Mesh(sunGeometry, sunMaterial);
sun.position.x = 0;
sun.position.y = 0;
sun.position.z = 0;
scene.add(sun);

const merkGeometry = new THREE.SphereGeometry(0.2, 12, 13);
const merkMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const merk = new THREE.Mesh(merkGeometry, merkMaterial);
merk.position.x = 5;
merk.position.y = 0;
merk.position.z = 0;
scene.add(merk);

const venGeometry = new THREE.SphereGeometry(0.4, 12, 13);
const venMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const ven = new THREE.Mesh(venGeometry, venMaterial);
ven.position.x = 7;
ven.position.y = 0;
ven.position.z = 0;
scene.add(ven);

const earthGeometry = new THREE.SphereGeometry(0.4, 12, 13);
const earthMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const earth = new THREE.Mesh(earthGeometry, earthMaterial);
earth.position.x = 10;
earth.position.y = 0;
earth.position.z = 0;
scene.add(earth);

const marsGeometry = new THREE.SphereGeometry(0.2, 12, 13);
const marsMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const mars = new THREE.Mesh(marsGeometry, marsMaterial);
mars.position.x = 12;
mars.position.y = 0;
mars.position.z = 0;
scene.add(mars);

const upitGeometry = new THREE.SphereGeometry(0.8, 12, 13);
const upitMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const upit = new THREE.Mesh(upitGeometry, upitMaterial);
upit.position.x = 15;
upit.position.y = 0;
upit.position.z = 0;
scene.add(upit);

const satGeometry = new THREE.SphereGeometry(0.7, 12, 13);
const satMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const sat = new THREE.Mesh(satGeometry, satMaterial);
sat.position.x = 18;
sat.position.y = 0;
sat.position.z = 0;
scene.add(sat);

const urGeometry = new THREE.SphereGeometry(0.5, 12, 13);
const urMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const ur = new THREE.Mesh(urGeometry, urMaterial);
ur.position.x = 21;
ur.position.y = 0;
ur.position.z = 0;
scene.add(ur);

const nepGeometry = new THREE.SphereGeometry(0.5, 12, 13);
const nepMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const nep = new THREE.Mesh(nepGeometry, nepMaterial);
nep.position.x = 23.5;
nep.position.y = 0;
nep.position.z = 0;
scene.add(nep);

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