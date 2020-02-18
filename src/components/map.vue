<template>
  <div class="map"></div>
</template>

<script>
import * as THREE from "three";

export default {
  name: "Map",
  props: {},
  data() {
    return {
      camera: null,
      scene: null,
      loader: null,
      renderer: null,
      mesh: null,
      light: null,
      sun: null,
      merk: null,
      ven: null,
      earth: null,
      mars: null,
      upit: null,
      sat: null,
      ur: null,
      nep: null
    };
  },
  methods: {
    init: function() {
      this.renderer = new THREE.WebGLRenderer({
        alpha: true,
        antialias: true
      }); //создаем рендер
      this.renderer.setSize(window.innerWidth, window.innerHeight); //размер сцены по окну
      document.body.appendChild(this.renderer.domElement); //вставляем в дом

      const color = 0x000000;
      const intensity = 1;
      this.light = new THREE.AmbientLight(color, intensity);

      //создаем камеру
      this.camera = new THREE.PerspectiveCamera(
        5, //поле зрения
        window.innerWidth / window.innerHeight, //aspectRatio
        1, //ближайший объект
        10000 //дальнейший объект
      );
      this.camera.position.set(0, 0, 100); //позиция камеры xyz
      this.camera.lookAt(0, 0, 0); //цель камеры

      this.scene = new THREE.Scene(); //создаем сцену
      this.loader = new THREE.TextureLoader(); //создаем загрузчик текстур
      this.scene.fog = new THREE.Fog(0xffffff, 1, 950); //добавляем туман
      this.scene.add(this.light);

      //солнце
      const sunGeometry = new THREE.SphereGeometry(1, 64, 64); //фигура солнца
      const sunMaterial = new THREE.MeshBasicMaterial({
        //текстура солнца
        map: this.loader.load(
          "https://thumbs.dreamstime.com/b/%D1%82%D0%B5%D0%BA%D1%81%D1%82%D1%83%D1%80%D0%B0-%D1%81%D0%BE-%D0%BD%D0%B5%D1%87%D0%BD%D0%B0%D1%8F-%D0%BF%D0%BE%D0%B2%D0%B5%D1%80%D1%85%D0%BD%D0%BE%D1%81%D1%82%D1%8C-65738086.jpg"
        )
      });
      this.sun = new THREE.Mesh(sunGeometry, sunMaterial); //модель солнца
      this.sun.position.x = 0;
      this.sun.position.y = 0;
      this.sun.position.z = 0;
      this.scene.add(this.sun); //вводим солцне на сцену

      //меркурий
      const merkGeometry = new THREE.SphereGeometry(0.05, 64, 64);
      const merkMaterial = new THREE.MeshBasicMaterial({
        map: this.loader.load(
          "https://avatars.mds.yandex.net/get-pdb/1623506/cc2c8ccc-4aa2-46f3-b5d5-3c0e5910af12/s600"
        )
      });
      this.merk = new THREE.Mesh(merkGeometry, merkMaterial);
      this.merk.position.x = 1.5;
      this.merk.position.y = 0;
      this.merk.position.z = 0;
      this.scene.add(this.merk);

      //венера
      const venGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const venMaterial = new THREE.MeshBasicMaterial({
        map: this.loader.load(
          "https://topling61.ru/images/detailed/12/p52182_1003092_shahti_plitka_napolnaya_330330_venera_palevaya_kg_.jpg"
        )
      });
      this.ven = new THREE.Mesh(venGeometry, venMaterial);
      this.ven.position.x = 2.2;
      this.ven.position.y = 0;
      this.ven.position.z = 0;
      this.scene.add(this.ven);

      //земля
      const earthGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const earthMaterial = new THREE.MeshBasicMaterial({
        map: this.loader.load(
          "https://img1.goodfon.ru/wallpaper/big/3/bb/planeta-zemlya-kosmos-triple.jpg"
        )
      });
      this.earth = new THREE.Mesh(earthGeometry, earthMaterial);
      this.earth.position.x = 3;
      this.earth.position.y = 0;
      this.earth.position.z = 0;
      this.scene.add(this.earth);

      //марс
      const marsGeometry = new THREE.SphereGeometry(0.09, 64, 64);
      const marsMaterial = new THREE.MeshBasicMaterial({
        map: this.loader.load(
          "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRnVWK2LKWCSD8Ix8L8NfzJevTVH3RkJYIAbElxkCYktkolUVlu"
        )
      });
      this.mars = new THREE.Mesh(marsGeometry, marsMaterial);
      this.mars.position.x = 3.7;
      this.mars.position.y = 0;
      this.mars.position.z = 0;
      this.scene.add(this.mars);

      //юпитер
      const upitGeometry = new THREE.SphereGeometry(0.28, 64, 64);
      const upitMaterial = new THREE.MeshBasicMaterial({ color: 0xffffff });
      this.upit = new THREE.Mesh(upitGeometry, upitMaterial);
      this.upit.position.x = 4.5;
      this.upit.position.y = 0;
      this.upit.position.z = 0;
      this.scene.add(this.upit);

      //сатурн
      const satGeometry = new THREE.SphereGeometry(0.25, 64, 64);
      const satMaterial = new THREE.MeshBasicMaterial({ color: 0xffffff });
      this.sat = new THREE.Mesh(satGeometry, satMaterial);
      this.sat.position.x = 5.4;
      this.sat.position.y = 0;
      this.sat.position.z = 0;
      this.scene.add(this.sat);

      //уран
      const urGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const urMaterial = new THREE.MeshBasicMaterial({ color: 0xffffff });
      this.ur = new THREE.Mesh(urGeometry, urMaterial);
      this.ur.position.x = 6.1;
      this.ur.position.y = 0;
      this.ur.position.z = 0;
      this.scene.add(this.ur);

      //нептун
      const nepGeometry = new THREE.SphereGeometry(0.15, 64, 64);
      const nepMaterial = new THREE.MeshBasicMaterial({ color: 0xffffff });
      this.nep = new THREE.Mesh(nepGeometry, nepMaterial);
      this.nep.position.x = 6.6;
      this.nep.position.y = 0;
      this.nep.position.z = 0;
      this.scene.add(this.nep);
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

      this.renderer.render(this.scene, this.camera); //рендерим
    }
  },
  mounted() {
    this.init();
    this.animate();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>