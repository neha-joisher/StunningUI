<template>
  <div class="min-h-screen bg-gradient-to-b from-black via-black to-neutral-900" id="app">
    <Header />
    <HeroSection />
    <FeatureGlobe />
    <Testimonials />
    <CallToAction />
    <ConfettiCelebration />
    <Footer />
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import HeroSection from './components/HeroSection.vue'
import Testimonials from './components/Testimonials.vue'
import FeatureGlobe from './components/FeatureGlobe.vue'
import ConfettiCelebration from './components/ConfettiCelebration.vue'
</script>

<style>

</style>

