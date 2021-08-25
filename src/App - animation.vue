<template>
  <canvas class="webgl"></canvas>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import * as THREE from 'three';
import gsap from 'gsap';

export default {
  data () {
    return {
      msg: 'hi'
    }
  },
  mounted () {
    this.createScene();
  },
  methods: {
    createScene () {
      const scene = new THREE.Scene();


      const cube1 = new THREE.Mesh(
        new THREE.BoxGeometry(1, 1, 1),
        new THREE.MeshBasicMaterial({color: 0xff0000})
      );

      scene.add(cube1);

      const sizes = {
        width: 800,
        height: 600
      };

      const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height);
      camera.position.z = 3;

      scene.add(camera);

      const canvas = document.querySelector('.webgl');
      const renderer = new THREE.WebGLRenderer({
        canvas: canvas
      });
      renderer.setSize(sizes.width, sizes.height);

      gsap.to(cube1.position, {duration: 1, delay: 1, x: 2});
      gsap.to(cube1.position, {duration: 1, delay: 2, x: 0});

      const tick = () => {
        renderer.render(scene, camera);

        window.requestAnimationFrame(tick);
      }
      tick();
    }
  }
}
</script>

<style>
</style>
