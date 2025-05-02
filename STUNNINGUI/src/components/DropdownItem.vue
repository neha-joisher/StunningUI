<template>
    <div class="flex items-start space-x-3 hover:bg-gray-50 p-2 rounded-md transition">
      <div class="text-xl">📌</div>
      <div>
        <p class="font-semibold">{{ title }}</p>
        <p class="text-sm text-gray-500">{{ desc }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    title: String,
    desc: String
  })
  </script>
  