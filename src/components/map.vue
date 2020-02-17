<template>
  <div class="map"></div>
</template>

<script>
import * as THREE from "three";

const renderer = new THREE.WebGLRenderer({ alpha: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

let camera = new THREE.PerspectiveCamera(
  30,
  window.innerWidth / window.innerHeight,
  1,
  1000
);
camera.position.set(0, 0, 100);
camera.lookAt(0, 0, 0);

const scene = new THREE.Scene();
const loader = new THREE.TextureLoader();

const sunGeometry = new THREE.SphereGeometry(1, 22, 23);
const sunMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://thumbs.dreamstime.com/b/%D1%82%D0%B5%D0%BA%D1%81%D1%82%D1%83%D1%80%D0%B0-%D1%81%D0%BE-%D0%BD%D0%B5%D1%87%D0%BD%D0%B0%D1%8F-%D0%BF%D0%BE%D0%B2%D0%B5%D1%80%D1%85%D0%BD%D0%BE%D1%81%D1%82%D1%8C-65738086.jpg"
  )
});
const sun = new THREE.Mesh(sunGeometry, sunMaterial);
sun.position.x = 0;
sun.position.y = 0;
sun.position.z = 0;
scene.add(sun);

const merkGeometry = new THREE.SphereGeometry(0.05, 12, 13);
const merkMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://avatars.mds.yandex.net/get-pdb/1623506/cc2c8ccc-4aa2-46f3-b5d5-3c0e5910af12/s600"
  )
});
const merk = new THREE.Mesh(merkGeometry, merkMaterial);
merk.position.x = 1.5;
merk.position.y = 0;
merk.position.z = 0;
scene.add(merk);

const venGeometry = new THREE.SphereGeometry(0.15, 12, 13);
const venMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://topling61.ru/images/detailed/12/p52182_1003092_shahti_plitka_napolnaya_330330_venera_palevaya_kg_.jpg"
  )
});
const ven = new THREE.Mesh(venGeometry, venMaterial);
ven.position.x = 2.2;
ven.position.y = 0;
ven.position.z = 0;
scene.add(ven);

const earthGeometry = new THREE.SphereGeometry(0.15, 12, 13);
const earthMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://img1.goodfon.ru/wallpaper/big/3/bb/planeta-zemlya-kosmos-triple.jpg"
  )
});
const earth = new THREE.Mesh(earthGeometry, earthMaterial);
earth.position.x = 3;
earth.position.y = 0;
earth.position.z = 0;
scene.add(earth);

const marsGeometry = new THREE.SphereGeometry(0.09, 12, 13);
const marsMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRnVWK2LKWCSD8Ix8L8NfzJevTVH3RkJYIAbElxkCYktkolUVlu"
  )
});
const mars = new THREE.Mesh(marsGeometry, marsMaterial);
mars.position.x = 3.7;
mars.position.y = 0;
mars.position.z = 0;
scene.add(mars);

const upitGeometry = new THREE.SphereGeometry(0.28, 12, 13);
const upitMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://lh3.googleusercontent.com/proxy/0FIuvegnapKDpt8TGd83JGAz-bJTOavFFRTauh3dEW0HXAqhnNtQHnyIvTeahML456dtRde9UsKEmyEjqLO2tfAotpOQMFOh_Bru7wiYtvk6KuNXOUYlxFd8CxxSKosy8ui1DppS"
  )
});
const upit = new THREE.Mesh(upitGeometry, upitMaterial);
upit.position.x = 4.5;
upit.position.y = 0;
upit.position.z = 0;
scene.add(upit);

const satGeometry = new THREE.SphereGeometry(0.25, 12, 13);
const satMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://lh3.googleusercontent.com/proxy/Z1IduCqNO2nPCWaNPzvZaFjJ46RDkPdAAX3RE2_yn7FgHxHN0yqGlLaceuJe5-c3imLpldRVA9YSxStXVRIGXJgH_Jchtp2tXjVG5LhVb2OvUjFWYq4hKatLd-uFjSeBnN2XZbM"
  )
});
const sat = new THREE.Mesh(satGeometry, satMaterial);
sat.position.x = 5.4;
sat.position.y = 0;
sat.position.z = 0;
scene.add(sat);

const urGeometry = new THREE.SphereGeometry(0.15, 12, 13);
const urMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://lh3.googleusercontent.com/proxy/usJno2THzKLg8RJ1d1z3ZARdFjaRFYCr2P1bAZ8n0fLCVKfnrtODq5l86UHe--u_ZxCFsbhRFj_gZ_WW3-jVhv2l5bJ_uKlzXt0VwjcMuNJ3UXk7yCTbyQ"
  )
});
const ur = new THREE.Mesh(urGeometry, urMaterial);
ur.position.x = 6.1;
ur.position.y = 0;
ur.position.z = 0;
scene.add(ur);

const nepGeometry = new THREE.SphereGeometry(0.15, 12, 13);
const nepMaterial = new THREE.MeshBasicMaterial({
  map: loader.load(
    "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSAuw8_sIRYuTuGpT4xNBkLwjMW722ASTOYJearSo58OYtrXyRz"
  )
});
const nep = new THREE.Mesh(nepGeometry, nepMaterial);
nep.position.x = 6.6;
nep.position.y = 0;
nep.position.z = 0;
scene.add(nep);

camera.position.z = 15;

const animate = function() {
  requestAnimationFrame(animate);

  sun.rotation.y += 0.001;
  merk.rotation.y += 0.01;
  ven.rotation.y += 0.02;
  earth.rotation.y += 0.02;
  mars.rotation.y += 0.01;
  upit.rotation.y += 0.001;
  sat.rotation.y += 0.001;
  ur.rotation.y += 0.001;
  nep.rotation.y += 0.001;

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