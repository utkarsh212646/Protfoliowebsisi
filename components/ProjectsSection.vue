<template>
  <section id="projects" class="section bg-gray-50">
    <div class="container">
      <h2 class="text-4xl font-bold text-center mb-16">My Projects</h2>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="(project, index) in projects" 
          :key="index"
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="index * 200"
          class="group"
          @click="openModal(project)"
        >
          <div class="bg-white rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow cursor-pointer">
            <div class="relative aspect-video overflow-hidden">
              <img 
                :src="project.image" 
                :alt="project.title"
                class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-500"
              />
              <div class="absolute inset-0 bg-primary/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                <span class="text-white font-semibold">View Project</span>
              </div>
            </div>
            
            <div class="p-6">
              <h3 class="text-xl font-semibold mb-2">{{ project.title }}</h3>
              <p class="text-gray-600 mb-4">{{ project.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span 
                  v-for="tech in project.technologies" 
                  :key="tech"
                  class="px-3 py-1 bg-primary/10 text-primary rounded-full text-sm"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Project Modal -->
      <TransitionRoot appear :show="isModalOpen" as="template">
        <Dialog as="div" @close="closeModal" class="relative z-50">
          <TransitionChild
            enter="duration-300 ease-out"
            enter-from="opacity-0"
            enter-to="opacity-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100"
            leave-to="opacity-0"
          >
            <div class="fixed inset-0 bg-black/50" />
          </TransitionChild>

          <div class="fixed inset-0 overflow-y-auto">
            <div class="flex min-h-full items-center justify-center p-4">
              <TransitionChild
                enter="duration-300 ease-out"
                enter-from="opacity-0 scale-95"
                enter-to="opacity-100 scale-100"
                leave="duration-200 ease-in"
                leave-from="opacity-100 scale-100"
                leave-to="opacity-0 scale-95"
              >
                <DialogPanel class="w-full max-w-3xl bg-white rounded-2xl overflow-hidden">
                  <div v-if="selectedProject">
                    <img 
                      :src="selectedProject.image" 
                      :alt="selectedProject.title"
                      class="w-full aspect-video object-cover"
                    />
                    <div class="p-6">
                      <h3 class="text-2xl font-semibold mb-4">{{ selectedProject.title }}</h3>
                      <p class="text-gray-600 mb-6">{{ selectedProject.fullDescription }}</p>
                      <div class="flex justify-end gap-4">
                        <a 
                          v-if="selectedProject.demoUrl"
                          :href="selectedProject.demoUrl"
                          target="_blank"
                          class="btn btn-primary"
                        >
                          Live Demo
                        </a>
                        <a
                          v-if="selectedProject.githubUrl"
                          :href="selectedProject.githubUrl"
                          target="_blank"
                          class="btn bg-gray-800 text-white hover:bg-gray-700"
                        >
                          View Code
                        </a>
                      </div>
                    </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
} from '@headlessui/vue'

const isModalOpen = ref(false)
const selectedProject = ref(null)

const projects = [
  {
    title: 'E-commerce Platform',
    description: 'A modern e-commerce platform built with Vue.js and Node.js',
    fullDescription: 'A full-featured e-commerce platform with user authentication, product management, shopping cart, and payment integration.',
    image: '/project1.jpg',
    technologies: ['Vue.js', 'Node.js', 'MongoDB'],
    demoUrl: 'https://demo.example.com',
    githubUrl: 'https://github.com/yourusername/project'
  },
  {
    title: 'Task Management App',
    description: 'Collaborative task management application',
    fullDescription: 'A real-time task management application with team collaboration features, file sharing, and progress tracking.',
    image: '/project2.jpg',
    technologies: ['React', 'Firebase', 'Tailwind CSS'],
    demoUrl: 'https://demo.example.com',
    githubUrl: 'https://github.com/yourusername/project'
  },
  {
    title: 'Social Media Dashboard',
    description: 'Analytics dashboard for social media management',
    fullDescription: 'A comprehensive dashboard for managing and analyzing social media performance across multiple platforms.',
    image: '/project3.jpg',
    technologies: ['Vue.js', 'D3.js', 'Express'],
    demoUrl: 'https://demo.example.com',
    githubUrl: 'https://github.com/yourusername/project'
  }
]

const openModal = (project) => {
  selectedProject.value = project
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
  setTimeout(() => {
    selectedProject.value = null
  }, 200)
}
</script>