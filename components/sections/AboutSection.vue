<script setup lang="ts">
const highlights = [
  {
    icon: 'heroicons:light-bulb-20-solid',
    title: 'Strategic Thinking',
    description: 'Data-driven approaches to identify opportunities and solve complex business challenges.',
  },
  {
    icon: 'heroicons:hand-raised-20-solid',
    title: 'Hands-On Support',
    description: 'Direct involvement in implementation, not just advice from the sidelines.',
  },
  {
    icon: 'heroicons:arrow-trending-up-20-solid',
    title: 'Results Focused',
    description: 'Every strategy is measured against tangible outcomes and ROI.',
  },
]
</script>

<template>
  <section id="about" class="py-24 bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid lg:grid-cols-2 gap-16 items-center">
        <!-- Image Side -->
        <div class="relative">
          <div class="relative z-10">
            <!-- Main Image Container -->
            <div class="bg-gradient-to-br from-primary-500 to-primary-700 rounded-3xl p-1">
              <div class="bg-dark-100 rounded-3xl aspect-[4/5] overflow-hidden">
                <img src="/compressed_image.jpg" alt="Anatolii Petrenko" class="w-full h-full object-cover" />
              </div>
            </div>

            <!-- Experience Badge -->
            <div class="absolute -bottom-6 -right-6 bg-white rounded-2xl p-6 shadow-xl border border-dark-100">
              <div class="text-4xl font-bold text-primary-600 mb-1">15+</div>
              <div class="text-sm text-dark-500">Years of<br/>Experience</div>
            </div>

            <!-- Decorative Elements -->
            <div class="absolute -top-6 -left-6 w-24 h-24 bg-secondary-100 rounded-full -z-10"></div>
            <div class="absolute -bottom-10 left-20 w-16 h-16 bg-primary-100 rounded-full -z-10"></div>
          </div>
        </div>

        <!-- Content Side -->
        <div>
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            About Me
          </span>
          <h2 class="section-title mb-6">
            Empowering Entrepreneurs to
            <span class="gradient-text">Achieve More</span>
          </h2>

          <div class="prose prose-lg text-dark-600 mb-8">
            <p class="leading-relaxed">
              As a continual improvement strategist, I partner with mission-based entrepreneurs who are ready to transform themselves and the people they influence.
            </p>
            <p class="leading-relaxed">
              My approach combines proven marketing strategies, strategic partnerships, and business optimization techniques to create sustainable, long-term growth for your business.
            </p>
          </div>

          <!-- Highlights -->
          <div class="space-y-6 mb-8">
            <div
              v-for="highlight in highlights"
              :key="highlight.title"
              class="flex items-start space-x-4"
            >
              <div class="flex-shrink-0 w-12 h-12 bg-primary-100 rounded-xl flex items-center justify-center">
                <Icon :name="highlight.icon" class="w-6 h-6 text-primary-600" />
              </div>
              <div>
                <h4 class="font-semibold text-dark-900 mb-1">{{ highlight.title }}</h4>
                <p class="text-dark-500 text-sm">{{ highlight.description }}</p>
              </div>
            </div>
          </div>

          <div class="flex flex-col sm:flex-row gap-4">
            <NuxtLink to="/about" class="btn-primary">
              Learn More About Me
              <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
            </NuxtLink>
            <NuxtLink to="/contact" class="btn-secondary">
              Let's Connect
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
