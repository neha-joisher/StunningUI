<template>
    <section class="bg-neutral-900 px-4 py-24 text-center relative">
      <h2 class="text-4xl font-bold mb-10 text-neutral-800 dark:text-white"></h2>
      <div ref="globeContainer" class="w-full h-[500px] mx-auto max-w-6xl"></div>
    </section>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import Globe from 'globe.gl'
  
  const globeContainer = ref(null)
  
  onMounted(() => {
  const world = Globe()(globeContainer.value)
    .globeImageUrl('//unpkg.com/three-globe/example/img/earth-night.jpg')
    .bumpImageUrl('//unpkg.com/three-globe/example/img/earth-topology.png')
    .showAtmosphere(true)
    .atmosphereColor('#3a228a')
    .atmosphereAltitude(0.25)
    .backgroundColor('#000');

  // Disable zoom controls
  world.controls().enableZoom = false;

  // Auto-rotate
  world.controls().autoRotate = true;
  world.controls().autoRotateSpeed = 0.4; // Adjust speed as needed

  // Optional: center the view initially
  world.pointOfView({ lat: 0, lng: 0, altitude: 2 }, 0);
});

  </script>
  
  <style scoped>
  </style>
  