<template>
  <section id="home" class="min-h-screen flex items-center relative overflow-hidden">
    <div class="container mx-auto px-4 pt-16">
      <div class="max-w-3xl mx-auto text-center">
        <h1 
          class="text-5xl md:text-7xl font-bold mb-6"
          v-motion
          :initial="{ opacity: 0, y: 100 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="200"
        >
          Hi, I'm <span class="text-primary">Your Name</span>
        </h1>
        
        <p 
          class="text-xl md:text-2xl text-gray-600 mb-8"
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="400"
        >
          Full Stack Developer & UI/UX Designer
        </p>
        
        <div
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="600"
        >
          <a 
            href="#contact"
            class="btn btn-primary inline-flex items-center group"
          >
            Let's Connect
            <ArrowRightIcon class="w-5 h-5 ml-2 group-hover:translate-x-1 transition-transform" />
          </a>
        </div>
      </div>
    </div>
    
    <!-- Animated background -->
    <div class="absolute inset-0 -z-10">
      <div class="absolute inset-0 bg-gradient-to-br from-blue-50 to-indigo-50"></div>
      <div class="absolute inset-0" ref="particles"></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { ArrowRightIcon } from '@heroicons/vue/24/outline'
import { gsap } from 'gsap'

const particles = ref(null)

onMounted(() => {
  // Create animated particles
  for (let i = 0; i < 50; i++) {
    const particle = document.createElement('div')
    particle.className = 'absolute w-2 h-2 bg-primary/10 rounded-full'
    particles.value.appendChild(particle)
    
    gsap.set(particle, {
      x: Math.random() * window.innerWidth,
      y: Math.random() * window.innerHeight
    })
    
    gsap.to(particle, {
      duration: 'random(2, 4)',
      y: '+=100',
      x: '+=50',
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut'
    })
  }
})
</script>