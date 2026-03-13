<script setup lang="ts">
const projects = [
  {
    title: 'AI Automation for Business Growth',
    description: 'Building powerful AI automation systems — from workflow automation to intelligent chatbots and API integrations.',
    image: '/serve.png',
    stack: [
      { name: 'PHP', icon: 'logos:php' },
      { name: 'Node.js', icon: 'logos:nodejs-icon' },
      { name: 'API', icon: 'heroicons:globe-alt-20-solid' },
      { name: 'JavaScript', icon: 'logos:javascript' },
    ],
  },
  {
    title: 'Elegant Styles — Modern Glamour Collection',
    description: 'A captivating fashion e-commerce platform with luxurious aesthetics and high-end visual identity.',
    image: '/clothes.png',
    stack: [
      { name: 'PHP', icon: 'logos:php' },
      { name: 'Laravel', icon: 'logos:laravel' },
      { name: 'MySQL', icon: 'logos:mysql' },
      { name: 'AWS', icon: 'logos:aws' },
      { name: 'Vue.js', icon: 'logos:vue' },
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
          <div class="aspect-[4/3] overflow-hidden">
            <img
              :src="project.image"
              :alt="project.title"
              class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-500"
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
                <div class="w-10 h-10 bg-white rounded-xl shadow-md border border-dark-100 flex items-center justify-center transform transition-all duration-300 hover:scale-110 hover:-translate-y-0.5 hover:border-primary-200 cursor-default">
                  <Icon :name="tech.icon" class="w-6 h-6" />
                </div>
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
