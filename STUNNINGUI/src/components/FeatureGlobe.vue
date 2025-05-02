<template>
  <section class="relative overflow-hidden bg-black min-h-[80vh] flex justify-center items-center">
    <div
      ref="globeContainer"
      class="globe-wrapper"
    ></div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import Globe from 'globe.gl'

const globeContainer = ref(null)
let world = null;

onMounted(() => {
  // Set the container size
  const containerWidth = window.innerWidth;
  const containerHeight = Math.min(window.innerHeight * 0.8, containerWidth);
  
  // Initialize globe
  world = Globe()
    .width(containerWidth)
    .height(containerHeight)
    (globeContainer.value)
    .globeImageUrl('https://unpkg.com/three-globe/example/img/earth-night.jpg')
    .bumpImageUrl('https://unpkg.com/three-globe/example/img/earth-topology.png')
    .showAtmosphere(true)
    .atmosphereColor('#3a228a')
    .atmosphereAltitude(0.25)
    .backgroundColor('#000');

  // Disable zoom controls
  world.controls().enableZoom = false;

  // Auto-rotate
  world.controls().autoRotate = true;
  world.controls().autoRotateSpeed = 0.4;

  // Center the view initially
  world.pointOfView({ lat: 0, lng: 0, altitude: 2 }, 0);
  
  // Handle window resize to keep globe centered
  window.addEventListener('resize', handleResize);
});

const handleResize = () => {
  if (world) {
    const containerWidth = window.innerWidth;
    const containerHeight = Math.min(window.innerHeight * 0.8, containerWidth);
    
    world
      .width(containerWidth)
      .height(containerHeight);
  }
};

onBeforeUnmount(() => {
  // Clean up event listener
  window.removeEventListener('resize', handleResize);
});
</script>

<style scoped>
.globe-wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

/* Target the canvas created by Globe.js */
.globe-wrapper :deep(canvas) {
  margin: 0 auto;
}
</style>