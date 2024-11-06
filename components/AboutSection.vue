<template>
  <section id="about" class="section bg-white">
    <div class="container">
      <h2 class="text-4xl font-bold text-center mb-16">About Me</h2>
      
      <div class="grid md:grid-cols-2 gap-12 items-center">
        <div 
          class="relative"
          v-motion
          :initial="{ opacity: 0, x: -50 }"
          :enter="{ opacity: 1, x: 0 }"
        >
          <div class="aspect-square rounded-2xl overflow-hidden">
            <img
              src="/placeholder-profile.jpg"
              alt="Your Name"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="absolute inset-0 bg-primary/10 rounded-2xl transform rotate-6 -z-10"></div>
        </div>
        
        <div
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0 }"
        >
          <h3 class="text-2xl font-semibold mb-4">Your Name</h3>
          <p class="text-gray-600 mb-6">
            A passionate developer with expertise in building modern web applications.
            I love creating beautiful and functional user experiences.
          </p>
          
          <div class="space-y-4">
            <div v-for="(item, index) in timeline" :key="index" class="flex gap-4">
              <div class="w-12 h-12 rounded-full bg-primary/10 flex items-center justify-center shrink-0">
                <component :is="item.icon" class="w-6 h-6 text-primary" />
              </div>
              <div>
                <h4 class="font-semibold">{{ item.title }}</h4>
                <p class="text-sm text-gray-600">{{ item.description }}</p>
                <span class="text-sm text-primary">{{ item.date }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { 
  AcademicCapIcon, 
  BriefcaseIcon,
  CommandLineIcon 
} from '@heroicons/vue/24/outline'

const timeline = [
  {
    title: 'Senior Developer',
    description: 'Leading development team at Tech Corp',
    date: '2020 - Present',
    icon: BriefcaseIcon
  },
  {
    title: 'Full Stack Developer',
    description: 'Building web applications at StartUp Inc',
    date: '2018 - 2020',
    icon: CommandLineIcon
  },
  {
    title: 'Computer Science Degree',
    description: 'University of Technology',
    date: '2014 - 2018',
    icon: AcademicCapIcon
  }
]
</script>