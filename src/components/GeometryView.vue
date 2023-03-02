<template>
  <div id="viewport" class="flex flex-col p-4">
    <div id="threejs-container" class="py-5"></div>
  </div>
</template>

<script setup>
// Imports;
import { onMounted, onUpdated } from "vue";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

// Property coming from parent component
const props = defineProps(["Radius", "Length", "CapSegment", "RadialSegment"]);

// Three js objects
let renderer, camera, scene, controls, geometry;

let width = 1200;
let heigh = 600;

function init() {
  // rendeder
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(width, heigh);
  renderer.setPixelRatio(window.devicePixelRatio);
  document.getElementById("threejs-container").appendChild(renderer.domElement);

  // camera
  camera = new THREE.PerspectiveCamera(45, width / heigh, 0.1, 1000);
  camera.position.set(40, 40, 40);
  

  // scene
  scene = new THREE.Scene();
  scene.background = new THREE.Color("#f65e5e");

  // orbit controls
  controls = new OrbitControls(camera, renderer.domElement);

  createcapsule(10,1,4);
  animate();

}

// for controls update
function animate() {
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);
}


function createcapsule(Radius, Length, CapSegment, RadialSegment) {
const geometry = new THREE.CapsuleGeometry( Radius, Length, CapSegment, RadialSegment );
const material = new THREE.MeshBasicMaterial({visible:props.bigcuboid});
const capsule = new THREE.Mesh( geometry, material );
scene.add( capsule );
}

function onSliderChange(color) {
  scene.clear();
  createcapsule(props.Radius, props.Length , props.CapSegment, props.RadialSegment);
}

// This function runs at the beginning of the component lifecycle.
// More about Vue lifecycles: https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram
onMounted(() => {
  init();
  animate();
});

// This function runs when DOM updates.
onUpdated(() => {
  // text content should be the same as current `count.value`
  onSliderChange();
});
</script>

<style scoped>
#viewport {
  background-color: hwb(300 69% 0%);
  border-style: dotted;
  border-color: #d2dfe8;
  border-width: 4px;
  border-radius: 10px;
  margin: 12px;
  height: 600px;
  width: 1200px;
  min-width: 200px;
  position: inherit;
}
</style>

