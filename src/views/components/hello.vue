<!--
 * @Description:  
 * @Author: owen
 * @Date: 2021-08-27 10:32:33
 * @LastEditTime: 2021-08-28 14:54:30
-->
<template>
  <canvas ref="webgl" class="webgl"></canvas>
</template>
<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
export default {
  name: "Hello",
  mounted() {
    const sizes = {
      width: window.innerWidth,
      height: window.innerHeight,
    };
    const canvas = this.$refs.webgl;
    const scene = new THREE.Scene();
    // eslint-disable-next-line prettier/prettier
    const camera = new THREE.PerspectiveCamera(45, sizes.width / sizes.height, 0.1, 1000);
    camera.position.set(5, 5, 20);
    scene.add(camera);

    const axesHelper = new THREE.AxesHelper();
    scene.add(axesHelper);

    const controls = new OrbitControls(camera, canvas);
    scene.add(controls);

    //球1
    const box = new THREE.SphereGeometry();
    const boxMaterial = new THREE.MeshNormalMaterial();
    const boxCube = new THREE.Mesh(box, boxMaterial);
    scene.add(boxCube);
    //球2
    const boxCube1 = new THREE.Mesh(box, boxMaterial);
    scene.add(boxCube1);
    //球3
    const boxCube2 = new THREE.Mesh(box, boxMaterial);
    scene.add(boxCube2);

    // const plan = new THREE.PlaneGeometry(200, 200);
    // const planCube = new THREE.Mesh(plan, boxMaterial);
    // planCube.rotation.x = -(Math.PI / 2);
    // scene.add(planCube);

    const renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
    renderer.setSize(sizes.width, sizes.height);
    renderer.setClearColor("#1abc9c");
    renderer.render(scene, camera);

    const clock = new THREE.Clock();
    const animate = () => {
      boxCube.position.x = Math.cos((clock.getElapsedTime() + 2) * 2) * 5;
      boxCube.position.z = Math.sin((clock.getElapsedTime() + 125) * 2) * 10;

      boxCube1.position.x = Math.cos((clock.getElapsedTime() + 4.24) * 2) * 5;
      boxCube1.position.y = Math.sin((clock.getElapsedTime() + 4) * 2) * 11;

      boxCube2.position.y = Math.cos((clock.getElapsedTime() + 2.7) * 2) * 5;
      boxCube2.position.z = Math.sin((clock.getElapsedTime() + 5.8) * 2) * 12;

      requestAnimationFrame(animate);
      controls.update();
      renderer.render(scene, camera);
    };
    animate();
  },
};
</script>
