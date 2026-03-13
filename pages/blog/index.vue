<script setup lang="ts">
useSeoMeta({
  title: 'Products | Anatolii Petrenko',
  description: 'Explore my portfolio of web applications, mobile apps, and AI-powered platforms built for real-world businesses.',
})

const projects = [
  {
    id: 'ecommerce-platform',
    title: 'E-Commerce Platform',
    description: 'A full-stack e-commerce solution with React, Node.js, and PostgreSQL featuring real-time inventory management and payment processing.',
    category: 'Web App',
    link: 'https://wolfandbadger.com',
    stack: [
      { name: 'React', icon: 'logos:react' },
      { name: 'Node.js', icon: 'logos:nodejs-icon' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
      { name: 'Stripe', icon: 'logos:stripe' },
    ],
  },
  {
    id: 'social-media-dashboard',
    title: 'Social Media Dashboard',
    description: 'A responsive social media analytics dashboard built with Next.js and TypeScript, featuring real-time data visualization.',
    category: 'Dashboard',
    link: 'https://poosting.com/',
    stack: [
      { name: 'Next.js', icon: 'logos:nextjs-icon' },
      { name: 'TypeScript', icon: 'logos:typescript-icon' },
      { name: 'Chart.js', icon: 'simple-icons:chartdotjs' },
      { name: 'Tailwind CSS', icon: 'logos:tailwindcss-icon' },
    ],
  },
  {
    id: 'real-estate-platform',
    title: 'Real Estate Platform',
    description: 'A comprehensive real estate platform with property listings, virtual tours, and advanced search functionality.',
    category: 'Web App',
    link: 'https://propertiesmt.com',
    stack: [
      { name: 'Next.js', icon: 'logos:nextjs-icon' },
      { name: 'Prisma', icon: 'simple-icons:prisma' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
      { name: 'Google Maps', icon: 'logos:google-maps' },
    ],
  },
  {
    id: 'task-management-app',
    title: 'Task Management Mobile App',
    description: 'A cross-platform mobile app for task management with offline capabilities and real-time synchronization.',
    category: 'Mobile App',
    link: 'https://mylifeorganized.net',
    stack: [
      { name: 'React Native', icon: 'logos:react' },
      { name: 'Firebase', icon: 'logos:firebase' },
      { name: 'Redux', icon: 'logos:redux' },
    ],
  },
  {
    id: 'ai-chatbot',
    title: 'AI-Powered Chatbot',
    description: 'An intelligent chatbot API built with Python and FastAPI, integrated with natural language processing capabilities.',
    category: 'AI',
    link: 'https://nomi.ai',
    stack: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'FastAPI', icon: 'simple-icons:fastapi' },
      { name: 'OpenAI', icon: 'simple-icons:openai' },
      { name: 'Docker', icon: 'logos:docker-icon' },
    ],
  },
  {
    id: 'weather-app',
    title: 'Weather Forecast App',
    description: 'A beautiful weather application with location-based forecasts and interactive weather maps.',
    category: 'Web App',
    link: 'https://weawow.com',
    stack: [
      { name: 'React', icon: 'logos:react' },
      { name: 'Leaflet', icon: 'logos:leaflet' },
      { name: 'CSS3', icon: 'logos:css-3' },
    ],
  },
]

const categories = ['All', 'Web App', 'Dashboard', 'Mobile App', 'AI']

const selectedCategory = ref('All')

const filteredProjects = computed(() => {
  if (selectedCategory.value === 'All') return projects
  return projects.filter(p => p.category === selectedCategory.value)
})

const categoryColors: Record<string, string> = {
  'Web App': 'bg-blue-100 text-blue-700',
  'Dashboard': 'bg-green-100 text-green-700',
  'Mobile App': 'bg-purple-100 text-purple-700',
  'AI': 'bg-orange-100 text-orange-700',
}
</script>

<template>
  <div>
    <!-- Hero -->
    <section class="pt-32 pb-20 bg-gradient-to-br from-dark-900 via-dark-800 to-primary-900 relative overflow-hidden">
      <div class="absolute inset-0">
        <div class="absolute top-1/4 -left-20 w-96 h-96 bg-primary-500/20 rounded-full blur-3xl"></div>
        <div class="absolute bottom-1/4 -right-20 w-80 h-80 bg-secondary-500/20 rounded-full blur-3xl"></div>
      </div>

      <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <span class="inline-block px-4 py-1.5 bg-white/10 text-primary-300 text-sm font-semibold rounded-full mb-6">
          Products
        </span>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-display text-white mb-6">
          Built &
          <span class="bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Delivered
          </span>
        </h1>
        <p class="text-xl text-dark-300 max-w-2xl mx-auto">
          A collection of real-world products I've built — from e-commerce platforms and dashboards to AI-powered systems and mobile apps.
        </p>
      </div>
    </section>

    <!-- Projects -->
    <section class="py-16 bg-dark-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <!-- Category Filter -->
        <div class="flex flex-wrap gap-2 mb-12">
          <button
            v-for="category in categories"
            :key="category"
            class="px-4 py-2 rounded-full text-sm font-medium transition-all"
            :class="selectedCategory === category
              ? 'bg-primary-600 text-white'
              : 'bg-white text-dark-600 hover:bg-dark-100'"
            @click="selectedCategory = category"
          >
            {{ category }}
          </button>
        </div>

        <!-- Projects Grid -->
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="project in filteredProjects"
            :key="project.id"
            class="group card overflow-hidden"
          >
            <!-- Header -->
            <div class="aspect-video bg-gradient-to-br from-primary-100 to-secondary-100 relative overflow-hidden flex items-center justify-center">
              <Icon name="heroicons:rocket-launch-20-solid" class="w-16 h-16 text-primary-300 group-hover:scale-110 transition-transform duration-300" />
              <div class="absolute inset-0 bg-dark-900/0 group-hover:bg-dark-900/10 transition-colors duration-300"></div>
            </div>

            <!-- Content -->
            <div class="p-6">
              <div class="flex items-center space-x-3 mb-4">
                <span
                  class="px-3 py-1 text-xs font-semibold rounded-full"
                  :class="categoryColors[project.category] || 'bg-dark-100 text-dark-600'"
                >
                  {{ project.category }}
                </span>
              </div>

              <h3 class="text-lg font-bold text-dark-900 mb-2 group-hover:text-primary-600 transition-colors">
                {{ project.title }}
              </h3>

              <p class="text-dark-500 text-sm mb-6 leading-relaxed">
                {{ project.description }}
              </p>

              <!-- Tech Stack -->
              <div class="flex flex-wrap gap-2 mb-6">
                <div
                  v-for="tech in project.stack"
                  :key="tech.name"
                  class="group/tech relative"
                >
                  <div class="w-9 h-9 bg-white rounded-lg shadow-sm border border-dark-100 flex items-center justify-center hover:scale-110 hover:-translate-y-0.5 hover:border-primary-200 transition-all duration-300 cursor-default">
                    <Icon :name="tech.icon" class="w-5 h-5" />
                  </div>
                  <div class="absolute -top-7 left-1/2 -translate-x-1/2 bg-dark-900 text-white text-xs px-2 py-0.5 rounded opacity-0 group-hover/tech:opacity-100 transition-opacity whitespace-nowrap pointer-events-none">
                    {{ tech.name }}
                  </div>
                </div>
              </div>

              <!-- Link -->
              <div class="pt-4 border-t border-dark-100">
                <a
                  :href="project.link"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="text-primary-600 font-semibold text-sm flex items-center hover:text-primary-700 transition-colors"
                >
                  Live Demo
                  <Icon name="heroicons:arrow-top-right-on-square-20-solid" class="w-4 h-4 ml-1" />
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Empty State -->
        <div v-if="filteredProjects.length === 0" class="text-center py-16">
          <Icon name="heroicons:document-magnifying-glass-20-solid" class="w-16 h-16 text-dark-300 mx-auto mb-4" />
          <h3 class="text-xl font-bold text-dark-900 mb-2">No projects found</h3>
          <p class="text-dark-500">Try selecting a different category.</p>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <section class="py-24 bg-white">
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <Icon name="heroicons:code-bracket-20-solid" class="w-16 h-16 text-primary-600 mx-auto mb-6" />
        <h2 class="section-title mb-4">
          Have a Project in <span class="gradient-text">Mind?</span>
        </h2>
        <p class="text-lg text-dark-500 mb-8">
          I'm always open to new challenges. Let's build something great together.
        </p>
        <NuxtLink to="/contact" class="btn-primary">
          Get In Touch
          <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
        </NuxtLink>
      </div>
    </section>
  </div>
</template>
