<template>
  <div id="viewport" class="flex flex-col p-4">
    <div id="threejs-container" class="py-5"></div>
  </div>
</template>

<script>
import * as THREE from 'three';

export default {
  data() {
    return {
      cuboidWidth: 1.5,
      cuboidHeight: 1,
      cuboidDepth: 0.5,
      cubeSize: 1,
      sphereRadius: 0.75,
    };
  },
  mounted() {
    // Create a Three.js scene
    const scene = new THREE.Scene();

    // Create a camera
    const camera = new THREE.PerspectiveCamera(
      75,
      this.$refs.container.clientWidth / this.$refs.container.clientHeight,
      0.1,
      1000
    );
    camera.position.z = 5;

    // Create a renderer
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(this.$refs.container.clientWidth, this.$refs.container.clientHeight);
    this.$refs.container.appendChild(renderer.domElement);

    // Create a cuboid
    const cuboidGeometry = new THREE.BoxGeometry(
      this.cuboidWidth,
      this.cuboidHeight,
      this.cuboidDepth
    );
    const cuboidMaterial = new THREE.MeshBasicMaterial({ color: 0xff0000 });
    const cuboid = new THREE.Mesh(cuboidGeometry, cuboidMaterial);
    cuboid.position.x = -2;
    scene.add(cuboid);

    // Create a cube
    const cubeGeometry = new THREE.BoxGeometry(this.cubeSize, this.cubeSize, this.cubeSize);
    const cubeMaterial = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
    scene.add(cube);

    // Create a sphere
    const sphereGeometry = new THREE.SphereGeometry(this.sphereRadius, 32, 32);
    const sphereMaterial = new THREE.MeshBasicMaterial({ color: 0x0000ff });
    const sphere = new THREE.Mesh(sphereGeometry, sphereMaterial);
    sphere.position.x = 2;
    scene.add(sphere);

    // Render the scene
    const animate = () => {
      requestAnimationFrame(animate);
      cuboid.scale.set(this.cuboidWidth, this.cuboidHeight, this.cuboidDepth);
      cube.scale.set(this.cubeSize, this.c
    