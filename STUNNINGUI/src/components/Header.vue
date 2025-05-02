<template>
    <header
      class="w-full fixed top-0 z-50 bg-white/80 backdrop-blur border-b border-neutral-200 dark:border-neutral-800"
    >
      <div class="max-w-screen-xl mx-auto flex justify-between items-center px-4 sm:px-8 h-16">
        <!-- Logo -->
        <a href="/" class="flex items-center gap-2">
          <MinimalLogo class="h-6 w-6 text-emerald-500" />
          <h1 class="text-xl font-bold text-primary">HumanitariansAI</h1>
        </a>
  
        <!-- Navigation and Buttons -->
        <div class="flex items-center gap-6">
          <!-- Dropdown -->
          <div class="relative" @mouseenter="showDropdown = true" @mouseleave="showDropdown = false">
            <button class="text-sm font-medium text-neutral-700 hover:text-black flex items-center gap-1">
              Projects <span>▾</span>
            </button>
            <div
              v-if="showDropdown"
              class="absolute top-full mt-2 left-0 w-64 p-4 bg-white rounded-md shadow-lg z-50 space-y-2 border"
            >
              <div class="hover:bg-neutral-50 p-2 rounded">
                <p class="font-semibold">Task</p>
                <p class="text-sm text-neutral-500">Celebrate the joy of accomplishment</p>
              </div>
              <div class="hover:bg-neutral-50 p-2 rounded">
                <p class="font-semibold">Dashboard</p>
                <p class="text-sm text-neutral-500">Gain insights with detailed reports</p>
              </div>
              <div class="hover:bg-neutral-50 p-2 rounded">
                <p class="font-semibold">Integrations</p>
                <p class="text-sm text-neutral-500">Manage with StunningUI tools</p>
              </div>
            </div>
          </div>
  
          <a href="#" class="text-sm font-medium text-neutral-700 hover:text-black">Services</a>
          <a href="#" class="text-sm font-medium text-neutral-700 hover:text-black">FAQ</a>
  
          <!-- Auth Buttons -->
          <div class="flex items-center gap-3 ml-6">
            <button class="text-sm font-medium text-neutral-700 hover:text-black">Sign in</button>
            <button class="text-sm bg-black text-white px-4 py-1.5 rounded-md hover:bg-neutral-900">
              Get started free
            </button>
          </div>
        </div>
      </div>
    </header>
  </template>
  
  
  <script lang="ts" setup>
  import { ref } from 'vue'
  const showDropdown = ref(false)
  </script>
  
  <style scoped></style>