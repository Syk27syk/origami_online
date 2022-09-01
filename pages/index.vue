<template>
  <div>
    <header class="grid grid-cols-2 bg-black text-white font-bold">
      <div id="logo" class="flex flex-row">
        <img src="/logo.png" class="h-20 w-20 m-5" alt="" />
        <p class="text-3xl font-bold my-auto">Origami Online</p>
      </div>
      <div id="navigation" class="grid grid-cols-4 my-auto text-2xl font-bold">
        <span>nav item 1</span>
        <span>nav item 2</span>
        <span>nav item 3</span>
        <span>nav item 4</span>
      </div>
    </header>
    <div class="flex h-screen h-[100vh] bg-[url('/hero-bg.jpg')] bg-cover bg-center align-middle text-white text-center">
      <div class="m-auto p-60 bg-black bg-opacity-30 rounded-full">
        <h1 class="text-5xl">Origami Online</h1>
        <p class="mt-5 text-3xl font-bold">fold origami virtually</p>
      </div>
    </div>
    <div id="bg">
      <canvas id="canvas" />
    </div>
    <footer class="bg-black text-white m-auto text-center">
      <p class="py-5 text-2xl font-bold">Made in Malaysia 2022</p>
    </footer>
  </div>
</template>

<script>
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';

export default {
  data() {
    return {
      camera: new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000),
      scene: new THREE.Scene(),
      renderer: new THREE.WebGLRenderer({
        canvas: document.querySelector('#canvas')
      }),
      mesh: null
    }
  },
  head() {
    return {
      script: [
        {
          async: true,
          src: 'https://unpkg.com/es-module-shims@1.3.6/dist/es-module-shims.js'
        },
        {
          type: 'importmap',
          imports: {
            three: 'https://unpkg.com/three@<version>/build/three.module.js'
          }
        },
      ]
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.camera.position.setZ(30);
      this.renderer.render(this.scene, this.camera);

      // add shapes//geometry //materials //mesh
      const geometry = new THREE.PlaneGeometry(10, 3, 16, 100)
      const material = new THREE.MeshBasicMaterial({ color: 0xFF6347, wireframe: true });
      const plane = new THREE.Mesh(geometry, material);
      const controls = new OrbitControls(this.camera, this.renderer.domElement);
      // renderer.render( scene, camera);

      // render
      this.scene.add(plane)

      // lighting
      const pointLight = new THREE.PointLight(0xFFFFFF)
      pointLight.position.set(5, 5, 5)
      // pointLight.position.set(20,20,20)

      const ambientLight = new THREE.AmbientLight(0xFFFFFF);
      this.scene.add(pointLight, ambientLight)

      const lightHelper = new THREE.PointLightHelper(pointLight)
      const gridHelper = new THREE.GridHelper(200, 50);
      this.scene.add(lightHelper, gridHelper)

      // animate
      function animate() {
        requestAnimationFrame(animate);

        plane.rotation.x += 0.01;
        plane.rotation.y += 0.005;
        plane.rotation.z += 0.01;

        controls.update();
        this.renderer.render(this.scene, this.camera);
      }

      animate()
    }
  },
}
</script>
