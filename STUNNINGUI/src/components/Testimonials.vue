<template>
<section class="relative py-12 bg-white dark:bg-neutral-950 z-10">
    <h2 class="text-2xl font-bold text-center mb-6 text-neutral-800 dark:text-white">What people are saying</h2>

    <!-- Scrollable container -->
    <div class="relative">
      <button
        @click="scrollLeft"
        class="absolute left-0 top-1/2 -translate-y-1/2 z-10 p-2 bg-white shadow rounded-full hover:bg-neutral-100 dark:bg-neutral-800 dark:hover:bg-neutral-700"
      >
        ◀
      </button>
      <div
        ref="scrollContainer"
        class="flex overflow-x-auto scroll-smooth snap-x snap-mandatory max-w-7xl mx-auto px-8 scrollbar-hide">
            <div
              v-for="(testimonial, index) in testimonials"
              :key="index"
              class="shrink-0 w-[400px] snap-start mx-3">
              <TestimonialCard
                :quote="testimonial.quote"
                :name="testimonial.name"
                :handle="testimonial.handle"
                :avatar="testimonial.avatar"
              />
            </div>
          </div>
      <button
        @click="scrollRight"
        class="absolute right-0 top-1/2 -translate-y-1/2 z-10 p-2 bg-white shadow rounded-full hover:bg-neutral-100 dark:bg-neutral-800 dark:hover:bg-neutral-700"
      >
        ▶
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import TestimonialCard from './stunning/TestimonialCard.vue'

const scrollContainer = ref(null)

const scrollLeft = () => {
  scrollContainer.value?.scrollBy({ left: -300, behavior: 'smooth' })
}

const scrollRight = () => {
  scrollContainer.value?.scrollBy({ left: 300, behavior: 'smooth' })
}

const testimonials = [
{
  quote: 'HumanitariansAI is redefining transparency!',
  name: 'Jane Doe',
  handle: 'janedoe',
  avatar: 'https://i.pravatar.cc/100?img=11'
},
{
  quote: 'Impressive mission and solid execution!',
  name: 'Amit Shah',
  handle: 'amitshah',
  avatar: 'https://i.pravatar.cc/100?img=12'
},
{
  quote: 'Amazing team, fast response, great product.',
  name: 'Lucy Wang',
  handle: 'lucyw',
  avatar: 'https://i.pravatar.cc/100?img=13'
}
]

</script>
