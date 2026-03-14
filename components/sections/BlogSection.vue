<script setup lang="ts">
const products = [
  {
    id: 'ecommerce-platform',
    title: 'E-Commerce Platform',
    description: 'A full-stack e-commerce solution with real-time inventory management and payment processing.',
    category: 'Web App',
    link: 'https://wolfandbadger.com',
    stack: [
      { name: 'React', icon: 'logos:react' },
      { name: 'Node.js', icon: 'logos:nodejs-icon' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
    ],
  },
  {
    id: 'social-media-dashboard',
    title: 'Social Media Dashboard',
    description: 'A responsive analytics dashboard with real-time data visualization and reporting.',
    category: 'Dashboard',
    link: 'https://poosting.com/',
    stack: [
      { name: 'Next.js', icon: 'logos:nextjs-icon' },
      { name: 'TypeScript', icon: 'logos:typescript-icon' },
      { name: 'Tailwind CSS', icon: 'logos:tailwindcss-icon' },
    ],
  },
  {
    id: 'ai-chatbot',
    title: 'AI-Powered Chatbot',
    description: 'An intelligent chatbot API with natural language processing for automated customer support.',
    category: 'AI',
    link: 'https://nomi.ai',
    stack: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'FastAPI', icon: 'simple-icons:fastapi' },
      { name: 'OpenAI', icon: 'simple-icons:openai' },
    ],
  },
]

const categoryColors: Record<string, string> = {
  'Web App': 'bg-blue-100 text-blue-700',
  'Dashboard': 'bg-green-100 text-green-700',
  'AI': 'bg-orange-100 text-orange-700',
}
</script>

<template>
  <section id="products" class="py-24 bg-dark-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="flex flex-col md:flex-row md:items-end md:justify-between mb-12">
        <div>
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            Products
          </span>
          <h2 class="section-title mb-4">
            Recent
            <span class="gradient-text">Products</span>
          </h2>
          <p class="section-subtitle">
            Real-world applications I've designed and shipped for clients.
          </p>
        </div>
        <NuxtLink to="/blog" class="btn-secondary mt-6 md:mt-0">
          View All Products
          <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
        </NuxtLink>
      </div>

      <!-- Products Grid -->
      <div class="grid md:grid-cols-3 gap-8">
        <div
          v-for="product in products"
          :key="product.id"
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
                :class="categoryColors[product.category] || 'bg-dark-100 text-dark-600'"
              >
                {{ product.category }}
              </span>
            </div>

            <h3 class="text-lg font-bold text-dark-900 mb-2 group-hover:text-primary-600 transition-colors">
              {{ product.title }}
            </h3>

            <p class="text-dark-500 text-sm mb-4 line-clamp-2">
              {{ product.description }}
            </p>

            <!-- Tech Stack -->
            <div class="flex flex-wrap gap-2 mb-4">
              <div
                v-for="tech in product.stack"
                :key="tech.name"
                class="group/tech relative"
              >
                <div class="w-8 h-8 bg-white rounded-lg shadow-sm border border-dark-100 flex items-center justify-center hover:scale-110 hover:border-primary-200 transition-all duration-300 cursor-default">
                  <Icon :name="tech.icon" class="w-4 h-4" />
                </div>
                <div class="absolute -top-7 left-1/2 -translate-x-1/2 bg-dark-900 text-white text-xs px-2 py-0.5 rounded opacity-0 group-hover/tech:opacity-100 transition-opacity whitespace-nowrap pointer-events-none">
                  {{ tech.name }}
                </div>
              </div>
            </div>

            <div class="pt-4 border-t border-dark-100">
              <a
                :href="product.link"
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
    </div>
  </section>
</template>
