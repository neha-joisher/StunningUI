<template>
    <div class="flex flex-col items-center h-[40vh] justify-center  bg-gradient-to-r from-purple-500 to-pink-500 text-white p-6">
      <h1 class="text-6xl font-bold mb-4">Ready to start your Journey?</h1>
      <button
        @click="launchConfetti"
        class="bg-white text-purple-600 font-semibold px-9 py-6  text-lg rounded-full shadow-lg hover:bg-gray-100 transition"
      >
        Join Now
      </button>
      <canvas ref="confettiCanvas" class="fixed inset-0 pointer-events-none"></canvas>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import confetti from 'canvas-confetti';
  
  const confettiCanvas = ref(null);
  let confettiInstance = null;
  
  onMounted(() => {
    if (confettiCanvas.value) {
      confettiInstance = confetti.create(confettiCanvas.value, {
        resize: true,
        useWorker: true,
      });
    }
  });
  
  const launchConfetti = () => {
    if (confettiInstance) {
      confettiInstance({
        particleCount: 150,
        spread: 70,
        origin: { y: 0.6 },
      });
    }
  };
  </script>
  
  <style scoped>
  /* Optional: Customize canvas to cover the entire screen */
  canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 9999;
  }
  </style>
  