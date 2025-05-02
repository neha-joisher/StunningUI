<template>
  <div class="max-w-xl mx-auto rounded-xl border border-neutral-200 dark:border-neutral-800 p-4 shadow-sm hover:shadow-md transition bg-white dark:bg-neutral-900">
    <div class="flex gap-4 items-start">
      <img
        :src="avatar"
        class="w-10 h-10 rounded-full"
        alt="Avatar"
      />
      <div class="flex-1">
        <div class="flex justify-between items-center">
          <div class="flex flex-col sm:flex-row sm:items-center gap-1 sm:gap-2">
            <p class="font-semibold text-neutral-800 dark:text-neutral-200">{{ name }}</p>
            <p class="text-sm text-neutral-500">@{{ handle }}</p>
          </div>
          <p class="text-sm text-neutral-400">2h</p>
        </div>
        <p class="mt-2 text-neutral-700 dark:text-neutral-300">
          {{ quote }}
        </p>
        <div class="flex gap-6 mt-4 text-neutral-500 dark:text-neutral-400 text-sm">
          <div class="flex items-center gap-2 cursor-pointer hover:text-blue-500 transition">
            💬 <span>12</span>
          </div>
          <div class="flex items-center gap-2 cursor-pointer hover:text-green-500 transition">
            🔁 <span>7</span>
          </div>
          <div class="flex items-center gap-2 cursor-pointer hover:text-pink-500 transition">
            ❤️ <span>34</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  quote: String,
  name: String,
  handle: String,
  avatar: String
})
</script>
