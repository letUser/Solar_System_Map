<template>
  <div class="map"></div>
</template>

<script>
import * as THREE from "three";
import { TrackballControls } from "three/examples/jsm/controls/TrackballControls.js";

export default {
  name: "Map",
  props: {},
  data() {
    return {
      camera: null,
      scene: null,
      loader: null,
      controls: null,
      renderer: null,
      mesh: null,
      light: null,
      ambLight: null,
      sun: null,
      merk: null,
      ven: null,
      earth: null,
      mars: null,
      upit: null,
      sat: null,
      ur: null,
      nep: null,
      currentAngle: 0
    };
  },
  methods: {
    init: function() {
      this.renderer = new THREE.WebGLRenderer(
        /* { alpha: true } */ { antialias: true }
      );
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.renderer.shadowMap.enabled = true;
      this.renderer.shadowMap.type = THREE.PCFSoftShadowMap;
      document.body.appendChild(this.renderer.domElement);
      this.camera = new THREE.PerspectiveCamera(
        5,
        window.innerWidth / window.innerHeight,
        0.1,
        3000
      );
      this.scene = new THREE.Scene();
      this.loader = new THREE.TextureLoader();
      this.controls = new TrackballControls(
        this.camera,
        this.renderer.domElement
      );
      this.controls.panSpeed = 0.02;
      this.controls.rotateSpeed = 1.5;
      this.controls.zoomSpeed = 2.4;

      this.camera.position.set(0, 20, 100);
      this.controls.update();

      /* МЕШЫ */
      const sunGeometry = new THREE.SphereGeometry(1, 64, 64);
      const sunMaterial = new THREE.MeshBasicMaterial({
        map: this.loader.load(
          "https://thumbs.dreamstime.com/b/%D1%82%D0%B5%D0%BA%D1%81%D1%82%D1%83%D1%80%D0%B0-%D1%81%D0%BE-%D0%BD%D0%B5%D1%87%D0%BD%D0%B0%D1%8F-%D0%BF%D0%BE%D0%B2%D0%B5%D1%80%D1%85%D0%BD%D0%BE%D1%81%D1%82%D1%8C-65738086.jpg"
        )
      });
      this.sun = new THREE.Mesh(sunGeometry, sunMaterial);
      this.sun.castShadow = true;
      this.sun.position.x = 0;
      this.sun.position.y = 0;
      this.sun.position.z = 0;
      this.scene.add(this.sun);
      const merkGeometry = new THREE.SphereGeometry(0.05, 64, 64);
      const merkMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://avatars.mds.yandex.net/get-pdb/1623506/cc2c8ccc-4aa2-46f3-b5d5-3c0e5910af12/s600"
        )
      });
      this.merk = new THREE.Mesh(merkGeometry, merkMaterial);
      this.merk.castShadow = true;
      this.merk.receiveShadow = true;
      this.scene.add(this.merk);
      const venGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const venMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://topling61.ru/images/detailed/12/p52182_1003092_shahti_plitka_napolnaya_330330_venera_palevaya_kg_.jpg"
        )
      });
      this.ven = new THREE.Mesh(venGeometry, venMaterial);
      this.ven.castShadow = true;
      this.ven.receiveShadow = true;
      this.scene.add(this.ven);

      const earthGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const earthMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://img1.goodfon.ru/wallpaper/big/3/bb/planeta-zemlya-kosmos-triple.jpg"
        )
      });
      this.earth = new THREE.Mesh(earthGeometry, earthMaterial);
      this.earth.castShadow = true;
      this.earth.receiveShadow = true;
      this.scene.add(this.earth);
      const marsGeometry = new THREE.SphereGeometry(0.09, 64, 64);
      const marsMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRnVWK2LKWCSD8Ix8L8NfzJevTVH3RkJYIAbElxkCYktkolUVlu"
        )
      });
      this.mars = new THREE.Mesh(marsGeometry, marsMaterial);
      this.mars.castShadow = true;
      this.mars.receiveShadow = true;
      this.scene.add(this.mars);
      const upitGeometry = new THREE.SphereGeometry(0.28, 64, 64);
      const upitMaterial = new THREE.MeshLambertMaterial(0xff0000);
      this.upit = new THREE.Mesh(upitGeometry, upitMaterial);
      this.upit.castShadow = true;
      this.upit.receiveShadow = true;
      this.scene.add(this.upit);
      const satGeometry = new THREE.SphereGeometry(0.25, 64, 64);
      const satMaterial = new THREE.MeshLambertMaterial(0xff0000);
      this.sat = new THREE.Mesh(satGeometry, satMaterial);
      this.sat.castShadow = true;
      this.sat.receiveShadow = true;
      this.scene.add(this.sat);
      const urGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const urMaterial = new THREE.MeshLambertMaterial(0xff0000);
      this.ur = new THREE.Mesh(urGeometry, urMaterial);
      this.ur.castShadow = true;
      this.ur.receiveShadow = true;
      this.scene.add(this.ur);
      const nepGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const nepMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSAuw8_sIRYuTuGpT4xNBkLwjMW722ASTOYJearSo58OYtrXyRz"
        )
      });
      this.nep = new THREE.Mesh(nepGeometry, nepMaterial);
      this.nep.castShadow = true;
      this.nep.receiveShadow = true;
      this.scene.add(this.nep);

      this.ambLight = new THREE.AmbientLight(0xffffff, 0.2);
      this.scene.add(this.ambLight);

      this.light = new THREE.PointLight(0xffffff, 1.8);
      this.light.position.set(0, 0, 0);
      this.renderer.physicallyCorrectLights = true;

      this.light.power = 25;
      this.light.decay = 2;
      this.light.distance = 50;
      this.scene.add(this.light);

      this.light.shadow.mapSize.width = 512;
      this.light.shadow.mapSize.height = 512;
      this.light.shadow.camera.near = 0.1;
      this.light.shadow.camera.far = 10000;

      var radius = 20;
      var radials = 16;
      var circles = 8;
      var divisions = 64;

      var helper2 = new THREE.PolarGridHelper(
        radius,
        radials,
        circles,
        divisions
      );
      this.scene.add(helper2);

      this.currentAngle = 0;
    },
    loop: function() {
      this.merk.position.x = 2.5 * Math.cos(this.currentAngle);
      this.merk.position.z = 2.5 * Math.sin(this.currentAngle);

      this.ven.position.x = 5 * Math.cos(this.currentAngle);
      this.ven.position.z = 5 * Math.sin(this.currentAngle);

      this.earth.position.x = 7.5 * Math.cos(this.currentAngle);
      this.earth.position.z = 7.5 * Math.sin(this.currentAngle);

      this.mars.position.x = 10 * Math.cos(this.currentAngle);
      this.mars.position.z = 10 * Math.sin(this.currentAngle);

      this.upit.position.x = 15 * Math.cos(this.currentAngle);
      this.upit.position.z = 15 * Math.sin(this.currentAngle);

      this.sat.position.x = 20 * Math.cos(this.currentAngle);
      this.sat.position.z = 20 * Math.sin(this.currentAngle);

      this.ur.position.x = 25 * Math.cos(this.currentAngle);
      this.ur.position.z = 25 * Math.sin(this.currentAngle);

      this.nep.position.x = 30 * Math.cos(this.currentAngle);
      this.nep.position.z = 30 * Math.sin(this.currentAngle);

      this.currentAngle += 0.01;
      this.renderer.render(this.scene, this.camera);

      requestAnimationFrame(this.loop);
    },
    animate: function() {
      requestAnimationFrame(this.animate);

      this.sun.rotation.y += 0.001;
      this.merk.rotation.y += 0.01;
      this.ven.rotation.y += 0.02;
      this.earth.rotation.y += 0.02;
      this.mars.rotation.y += 0.01;
      this.upit.rotation.y += 0.01;
      this.sat.rotation.y += 0.01;
      this.ur.rotation.y += 0.01;
      this.nep.rotation.y += 0.01;

      this.controls.update();

      this.renderer.render(this.scene, this.camera); //рендерим
    }
  },
  mounted() {
    this.init();
    this.loop();
    this.animate();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>