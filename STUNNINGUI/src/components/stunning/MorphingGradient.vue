<template>
    <div
      class="sui-morphing-gradient h-screen w-screen relative overflow-hidden top-0 left-0"
      ref="gradientWrapper"
      :style="wrapperStyle"
    >
      <!-- SVG filter for blur effect -->
      <svg xmlns="http://www.w3.org/2000/svg" class="hidden">
        <defs>
          <filter id="point">
            <feGaussianBlur in="SourceGraphic" stdDeviation="10" result="blur" />
            <feColorMatrix
              in="blur"
              mode="matrix"
              values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 18 -8"
              result="point"
            />
            <feBlend in="SourceGraphic" in2="point" />
          </filter>
        </defs>
      </svg>
  
      <!-- Glowy Button -->
      <div class="absolute inset-0 flex items-center justify-center mt-100 z-10">
      <button
           class="relative px-6 py-3 text-white font-semibold rounded-lg bg-black border border-transparent
           hover:scale-105 transition-all duration-300
           before:absolute before:inset-0 before:rounded-lg before:-z-10
           before:blur before:opacity-75 before:content-['']
           before:bg-gradient-to-r before:from-purple-500 before:via-pink-500 before:to-red-500">
       Get Started
      </button>
      </div>

  
      <!-- Gradient Layers -->
      <div class="gradients-container w-full h-full [filter:_url(#point)_blur(40px)]">
        <div class="g1"></div>
        <div class="g2"></div>
        <div class="g3"></div>
        <div class="g4"></div>
        <div class="g5"></div>
        <div class="interactive" ref="interactiveRef"></div>
      </div>
    </div>
  </template>
  
  
  <script lang="ts" setup>
  import { useMouse } from '@vueuse/core'
  import { ref, watch, toRefs, computed } from 'vue'
  
  const props = withDefaults(
    defineProps<{
      firstColor: string
      secondColor: string
      thirdColor: string
      fourthColor: string
      fifthColor: string
      interactiveColor: string
      interactive: boolean
      size: string
      mixBlendMode: string
    }>(),
    {
      firstColor: '18, 113, 255',
      secondColor: '221, 74, 255',
      thirdColor: '100, 220, 255',
      fourthColor: '200, 50, 50',
      fifthColor: '180, 180, 50',
      interactiveColor: '140, 100, 255',
      interactive: true,
      size: '80%',
      mixBlendMode: 'hard-light'
    }
  )
  
  const interactiveRef = ref<HTMLDivElement>()
  const { x, y } = useMouse()
  const currentPos = ref({ x: 0, y: 0 })
  const gradientWrapper = ref<HTMLDivElement | null>(null)
  
  const {
    firstColor,
    secondColor,
    thirdColor,
    fourthColor,
    fifthColor,
    interactiveColor,
    interactive,
    size,
    mixBlendMode
  } = toRefs(props)
  
  const wrapperStyle = computed(() => {
    return {
      '--color1': firstColor.value,
      '--color2': secondColor.value,
      '--color3': thirdColor.value,
      '--color4': fourthColor.value,
      '--color5': fifthColor.value,
      '--color-interactive': interactiveColor.value,
      '--circle-size': size.value,
      '--blending': mixBlendMode.value
    }
  })
  
  watch(
    () => [x.value, y.value],
    () => {
      if (!interactive.value) return
      if (!interactiveRef.value) return
      currentPos.value.x =
        currentPos.value.x + (x.value - currentPos.value.x) / 20
      currentPos.value.y =
        currentPos.value.y + (y.value - currentPos.value.y) / 20
      currentPos
      interactiveRef.value.style.transform = `translate(${Math.round(
        currentPos.value.x
      )}px, ${Math.round(currentPos.value.y)}px)`
    },
    {
      deep: true
    }
  )
  </script>
  
  <style scoped>
  .sui-morphing-gradient {
    --space: ;
    @supports (background: linear-gradient(in oklab, #000, #fff)) {
      --space: in oklab;
    }
    --color1: 18, 113, 255;
    --color2: 221, 74, 255;
    --color3: 100, 220, 255;
    --color4: 200, 50, 50;
    --color5: 180, 180, 50;
    --color-interactive: 140, 100, 255;
    --circle-size: 80%;
    --blending: hard-light;
  }
  
  @keyframes moveInCircle {
    0% {
      transform: rotate(0deg);
    }
    50% {
      transform: rotate(180deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  
  @keyframes moveVertical {
    0% {
      transform: translateY(-50%);
    }
    50% {
      transform: translateY(50%);
    }
    100% {
      transform: translateY(-50%);
    }
  }
  
  @keyframes moveHorizontal {
    0% {
      transform: translateX(-50%) translateY(-10%);
    }
    50% {
      transform: translateX(50%) translateY(10%);
    }
    100% {
      transform: translateX(-50%) translateY(-10%);
    }
  }
  
  .sui-morphing-gradient {
    .g1 {
      position: absolute;
      background: radial-gradient(
          circle at center,
          rgba(var(--color1), 0.8) 0,
          rgba(var(--color1), 0) 50%
        ) no-repeat;
      mix-blend-mode: var(--blending);
  
      width: var(--circle-size);
      height: var(--circle-size);
      top: calc(50% - var(--circle-size) / 2);
      left: calc(50% - var(--circle-size) / 2);
  
      transform-origin: center center;
      animation: moveVertical 30s ease infinite;
  
      opacity: 1;
    }
  
    .g2 {
      position: absolute;
      background: radial-gradient(
          circle at center,
          rgba(var(--color2), 0.8) 0,
          rgba(var(--color2), 0) 50%
        ) no-repeat;
      mix-blend-mode: var(--blending);
  
      width: var(--circle-size);
      height: var(--circle-size);
      top: calc(50% - var(--circle-size) / 2);
      left: calc(50% - var(--circle-size) / 2);
  
      transform-origin: calc(50% - 400px);
      animation: moveInCircle 20s reverse infinite;
  
      opacity: 1;
    }
  
    .g3 {
      position: absolute;
      background: radial-gradient(
          circle at center,
          rgba(var(--color3), 0.8) 0,
          rgba(var(--color3), 0) 50%
        ) no-repeat;
      mix-blend-mode: var(--blending);
  
      width: var(--circle-size);
      height: var(--circle-size);
      top: calc(50% - var(--circle-size) / 2 + 200px);
      left: calc(50% - var(--circle-size) / 2 - 500px);
  
      transform-origin: calc(50% + 400px);
      animation: moveInCircle 40s linear infinite;
  
      opacity: 1;
    }
  
    .g4 {
      position: absolute;
      background: radial-gradient(
          circle at center,
          rgba(var(--color4), 0.8) 0,
          rgba(var(--color4), 0) 50%
        ) no-repeat;
      mix-blend-mode: var(--blending);
  
      width: var(--circle-size);
      height: var(--circle-size);
      top: calc(50% - var(--circle-size) / 2);
      left: calc(50% - var(--circle-size) / 2);
  
      transform-origin: calc(50% - 200px);
      animation: moveHorizontal 40s ease infinite;
  
      opacity: 0.7;
    }
  
    .g5 {
      position: absolute;
      background: radial-gradient(
          circle at center,
          rgba(var(--color5), 0.8) 0,
          rgba(var(--color5), 0) 50%
        ) no-repeat;
      mix-blend-mode: var(--blending);
  
      width: calc(var(--circle-size) * 2);
      height: calc(var(--circle-size) * 2);
      top: calc(50% - var(--circle-size));
      left: calc(50% - var(--circle-size));
  
      transform-origin: calc(50% - 800px) calc(50% + 200px);
      animation: moveInCircle 20s ease infinite;
  
      opacity: 1;
    }
  
    .interactive {
      position: absolute;
      background: radial-gradient(
          circle at center,
          rgba(var(--color-interactive), 0.8) 0,
          rgba(var(--color-interactive), 0) 50%
        ) no-repeat;
      mix-blend-mode: var(--blending);
  
      width: 100%;
      height: 100%;
      top: -50%;
      left: -50%;
  
      opacity: 0.7;
    }
  }
  </style>
  