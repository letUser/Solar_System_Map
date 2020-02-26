<template>
  <div class="map"></div>
</template>

<script>
import * as THREE from "three";
import { TrackballControls } from "three/examples/jsm/controls/TrackballControls.js";
import { Astronomy } from "./calculations/astronomy.js";

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
      plut: null,
      currentAngle: 0,
      merkXYZ: null,
      venXYZ: null,
      earthXYZ: null,
      marsXYZ: null,
      upitXYZ: null,
      satXYZ: null,
      urXYZ: null,
      nepXYZ: null,
      plutXYZ: null
    };
  },
  methods: {
    init: function() {
      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.renderer.autoClearColor = false;
      this.renderer.shadowMap.enabled = true;
      this.renderer.shadowMap.type = THREE.PCFSoftShadowMap;
      this.renderer.getMaxAnisotropy();
      document.body.appendChild(this.renderer.domElement);
      this.camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.0001,
        1000
      );

      this.scene = new THREE.Scene();
      this.loader = new THREE.TextureLoader();
      this.controls = new TrackballControls(
        this.camera,
        this.renderer.domElement
      );
      this.controls.panSpeed = 0.5;
      this.controls.rotateSpeed = 1.5;
      this.controls.zoomSpeed = 1;

      this.camera.position.set(0, 0, 10);
      this.controls.update();

      this.scene.background = this.loader.load("./assets/space.jpg");

      /* МЕШЫ */
      const sunGeometry = new THREE.SphereGeometry(1, 64, 64);
      const sunMaterial = new THREE.MeshBasicMaterial({
        map: this.loader.load(
          "https://sun9-14.userapi.com/c205628/v205628419/7e86b/uET0t6HqLRU.jpg"
        )
      });
      this.sun = new THREE.Mesh(sunGeometry, sunMaterial);
      this.sun.castShadow = true;
      this.scene.add(this.sun);

      const merkGeometry = new THREE.SphereGeometry(0.05, 64, 64);
      const merkMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://sun9-16.userapi.com/c857020/v857020302/f482f/ADb7nwZAQdA.jpg"
        )
      });
      this.merk = new THREE.Mesh(merkGeometry, merkMaterial);
      this.merk.castShadow = true;
      this.merk.receiveShadow = true;
      this.scene.add(this.merk);
      const venGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const venMaterial = new THREE.MeshLambertMaterial({
        map: this.loader.load(
          "https://avatars.mds.yandex.net/get-pdb/1623506/cc2c8ccc-4aa2-46f3-b5d5-3c0e5910af12/s600"
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

      const plutGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const plutMaterial = new THREE.MeshLambertMaterial({
        alpha: true,
        color: 0x000000
      });
      this.plut = new THREE.Mesh(plutGeometry, plutMaterial);
      this.plut.castShadow = true;
      this.plut.receiveShadow = true;
      this.scene.add(this.plut);

      this.ambLight = new THREE.AmbientLight(0xffffff, 0.2);
      this.scene.add(this.ambLight);

      this.light = new THREE.PointLight(0xffffff, 1.8);
      this.light.position.set(0, 0, 0);
      this.renderer.physicallyCorrectLights = true;

      this.light.power = 25;
      this.light.decay = 2;
      this.light.distance = 1000;
      this.scene.add(this.light);

      this.light.shadow.mapSize.width = 512;
      this.light.shadow.mapSize.height = 512;
      this.light.shadow.camera.near = 0.1;
      this.light.shadow.camera.far = 10000;

      const loader = new THREE.CubeTextureLoader();
      const texture = loader.load([
        "https://sun9-30.userapi.com/c850608/v850608287/cfaad/0nK6n9jameQ.jpg",
        "https://sun9-31.userapi.com/c204828/v204828287/817ed/RlTe2zejDe8.jpg",
        "https://sun9-7.userapi.com/c205716/v205716287/82143/YcQBbbEjsJk.jpg",
        "https://sun9-2.userapi.com/c205128/v205128287/7fd29/VIULun-SDlo.jpg",
        "https://sun9-51.userapi.com/c857332/v857332287/832af/5nq9oRiR9r0.jpg",
        "https://sun9-63.userapi.com/c206824/v206824287/83f19/CLPSpstY-0w.jpg"
      ]);

      texture.minFilter = THREE.LinearFilter;
      texture.magFilter = THREE.LinearFilter;
      this.scene.background = texture;

      // let radius = 20;
      // let radials = 16;
      // let circles = 8;
      // let divisions = 64;

      // let helper2 = new THREE.PolarGridHelper(
      //   radius,
      //   radials,
      //   circles,
      //   divisions
      // );
      // this.scene.add(helper2);
    },
    calcGEO: function() {
      this.merkXYZ = Astronomy.Body[1].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.venXYZ = Astronomy.Body[2].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.earthXYZ = Astronomy.Body[3].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.marsXYZ = Astronomy.Body[5].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.upitXYZ = Astronomy.Body[16].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.satXYZ = Astronomy.Body[17].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.urXYZ = Astronomy.Body[18].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.nepXYZ = Astronomy.Body[19].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );
      this.plutXYZ = Astronomy.Body[20].EclipticCartesianCoordinates(
        Astronomy.DayValue(new Date())
      );

      setTimeout(() => this.calcGEO(), 600000); //обновляем данные каждые 10мин
    },
    loop: function() {
      this.merk.position.x = this.merkXYZ.x * 10;
      this.merk.position.y = this.merkXYZ.y * 10;
      this.merk.position.z = this.merkXYZ.z * 10;

      this.ven.position.x = this.venXYZ.x * 10;
      this.ven.position.y = this.venXYZ.y * 10;
      this.ven.position.z = this.venXYZ.z * 10;

      this.earth.position.x = this.earthXYZ.x * 10;
      this.earth.position.y = this.earthXYZ.y * 10;
      this.earth.position.z = this.earthXYZ.z * 10;

      this.mars.position.x = this.marsXYZ.x * 10;
      this.mars.position.y = this.marsXYZ.y * 10;
      this.mars.position.z = this.marsXYZ.z * 10;

      this.upit.position.x = this.upitXYZ.x * 10;
      this.upit.position.y = this.upitXYZ.y * 10;
      this.upit.position.z = this.upitXYZ.z * 10;

      this.sat.position.x = this.satXYZ.x * 10;
      this.sat.position.y = this.satXYZ.y * 10;
      this.sat.position.z = this.satXYZ.z * 10;

      this.ur.position.x = this.urXYZ.x * 10;
      this.ur.position.y = this.urXYZ.y * 10;
      this.ur.position.z = this.urXYZ.z * 10;

      this.nep.position.x = this.nepXYZ.x * 10;
      this.nep.position.y = this.nepXYZ.y * 10;
      this.nep.position.z = this.nepXYZ.z * 10;

      this.plut.position.x = this.plutXYZ.x * 10;
      this.plut.position.y = this.plutXYZ.y * 10;
      this.plut.position.z = this.plutXYZ.z * 10;

      this.renderer.render(this.scene, this.camera);

      this.currentAngle += 0.01;

      requestAnimationFrame(this.loop);
    },
    animate: function() {
      requestAnimationFrame(this.animate);

      this.merk.rotation.y += 0.00000005;
      this.ven.rotation.y += 0.000000001;
      this.earth.rotation.y += 0.000086;
      this.mars.rotation.y += 0.000086;
      this.upit.rotation.y += 0.000034;
      this.sat.rotation.y += 0.000036;
      this.ur.rotation.y += 0.000061;
      this.nep.rotation.y += 0.000057;
      this.plut.rotation.y += 0.0000000005;

      this.controls.update();

      this.renderer.render(this.scene, this.camera); //рендерим
    },
    resizeRendererToDisplaySize: function() {
      const canvas = this.renderer.domElement;
      const width = canvas.clientWidth;
      const height = canvas.clientHeight;
      const needResize = canvas.width !== width || canvas.height !== height;
      if (needResize) {
        this.renderer.setSize(width, height, false);
      }
      return needResize;
    },
    render: function() {
      if (this.resizeRendererToDisplaySize(this.renderer)) {
        const canvas = this.renderer.domElement;
        this.camera.aspect = canvas.clientWidth / canvas.clientHeight;
        this.camera.updateProjectionMatrix();
      }

      this.renderer.render(this.scene, this.camera);

      requestAnimationFrame(this.render);
    }
  },
  mounted() {
    this.init();
    this.calcGEO();
    this.loop();
    this.resizeRendererToDisplaySize();
    this.render();
    this.animate();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>


    // loop: function() {
    //   this.merk.position.x = this.merkXYZ.x;
    //   this.merk.position.y = this.merkXYZ.y;
    //   this.merk.position.z = this.merkXYZ.z;

    //   this.ven.position.x = this.venXYZ.x;
    //   this.ven.position.y = this.venXYZ.y;
    //   this.ven.position.z = this.venXYZ.z;

    //   this.earth.position.x = this.earthXYZ.x;
    //   this.earth.position.y = this.earthXYZ.y;
    //   this.earth.position.z = this.earthXYZ.z;

    //   this.mars.position.x = this.marsXYZ.x;
    //   this.mars.position.y = this.marsXYZ.y;
    //   this.mars.position.z = this.marsXYZ.z;

    //   this.upit.position.x = this.upitXYZ.x;
    //   this.upit.position.y = this.upitXYZ.y;
    //   this.upit.position.z = this.upitXYZ.z;

    //   this.sat.position.x =
    //     (1429394069 / 10000000) * Math.cos(this.currentAngle * 0.1);
    //   this.sat.position.z =
    //     (1429394069 / 10000000) * Math.sin(this.currentAngle * 0.1);

    //   this.ur.position.x =
    //     (2876679082 / 10000000) * Math.cos(this.currentAngle * 0.1);
    //   this.ur.position.z =
    //     (2876679082 / 10000000) * Math.sin(this.currentAngle * 0.1);

    //   this.nep.position.x =
    //     (4503443661 / 10000000) * Math.cos(this.currentAngle * 0.1);
    //   this.nep.position.z =
    //     (4503443661 / 10000000) * Math.sin(this.currentAngle * 0.1);

    //   if (this.currentAngle >= 62.8) this.currentAngle = 0;
    //   this.currentAngle += 0.01;
    //   this.renderer.render(this.scene, this.camera);

    //   requestAnimationFrame(this.loop);
    // },
