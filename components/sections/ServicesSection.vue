<script setup lang="ts">
const projects = [
  {
    title: 'AI Automation for Business Growth',
    description: 'Building powerful AI automation systems — from workflow automation to intelligent chatbots and API integrations.',
    image: '/serve.png',
    stack: [
      { name: 'PHP', color: 'from-indigo-500 to-indigo-700', letter: 'PHP' },
      { name: 'Node.js', color: 'from-green-500 to-green-700', letter: 'N' },
      { name: 'API', color: 'from-purple-500 to-purple-700', letter: 'API' },
      { name: 'JavaScript', color: 'from-yellow-400 to-yellow-600', letter: 'JS' },
    ],
  },
  {
    title: 'Elegant Styles — Modern Glamour Collection',
    description: 'A captivating fashion e-commerce platform with luxurious aesthetics and high-end visual identity.',
    image: '/clothes.png',
    stack: [
      { name: 'PHP', color: 'from-indigo-500 to-indigo-700', letter: 'PHP' },
      { name: 'Laravel', color: 'from-red-500 to-red-700', letter: 'L' },
      { name: 'MySQL', color: 'from-blue-500 to-blue-700', letter: 'My' },
      { name: 'AWS', color: 'from-orange-400 to-orange-600', letter: 'AWS' },
      { name: 'Vue.js', color: 'from-emerald-500 to-emerald-700', letter: 'V' },
    ],
  },
]
</script>

<template>
  <section id="services" class="py-24 bg-dark-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center mb-16">
        <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
          Portfolio
        </span>
        <h2 class="section-title mb-4">
          Recent
          <span class="gradient-text">Projects</span>
        </h2>
        <p class="section-subtitle mx-auto">
          Real-world solutions I've built for businesses — from AI automation to full-stack web platforms.
        </p>
      </div>

      <!-- Projects Grid -->
      <div class="grid md:grid-cols-2 gap-8">
        <div
          v-for="(project, index) in projects"
          :key="project.title"
          class="group card overflow-hidden hover:shadow-2xl"
          :style="{ animationDelay: `${index * 100}ms` }"
        >
          <!-- Image -->
          <div class="aspect-video overflow-hidden">
            <img
              :src="project.image"
              :alt="project.title"
              class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
            />
          </div>

          <!-- Content -->
          <div class="p-8">
            <h3 class="text-xl font-bold text-dark-900 mb-2 group-hover:text-primary-600 transition-colors">
              {{ project.title }}
            </h3>
            <p class="text-dark-500 mb-6 leading-relaxed">
              {{ project.description }}
            </p>

            <!-- Tech Stack -->
            <div class="flex flex-wrap gap-2">
              <div
                v-for="tech in project.stack"
                :key="tech.name"
                class="group/tech relative"
              >
                <div
                  class="w-10 h-10 rounded-lg bg-gradient-to-br shadow-md flex items-center justify-center text-white font-bold text-xs transform transition-all duration-300 hover:scale-110 hover:-translate-y-0.5 cursor-default"
                  :class="tech.color"
                >
                  {{ tech.letter }}
                </div>
                <!-- Tooltip -->
                <div class="absolute -top-7 left-1/2 -translate-x-1/2 bg-dark-900 text-white text-xs px-2 py-0.5 rounded opacity-0 group-hover/tech:opacity-100 transition-opacity whitespace-nowrap pointer-events-none">
                  {{ tech.name }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- CTA -->
      <div class="text-center mt-12">
        <NuxtLink to="/services" class="btn-primary">
          View All Projects
          <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
        </NuxtLink>
      </div>
    </div>
  </section>
</template>
