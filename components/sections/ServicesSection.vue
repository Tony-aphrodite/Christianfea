<script setup lang="ts">
const services = [
  {
    icon: 'heroicons:rocket-launch-20-solid',
    title: 'Business Growth Strategy',
    description: 'Develop a comprehensive roadmap for sustainable growth with actionable strategies tailored to your unique business goals.',
    features: ['Market Analysis', 'Growth Planning', 'Performance Metrics'],
    color: 'primary',
  },
  {
    icon: 'heroicons:user-group-20-solid',
    title: 'Referral Marketing',
    description: 'Harness the power of word-of-mouth marketing to generate high-quality leads and build lasting customer relationships.',
    features: ['Referral Programs', 'Customer Advocacy', 'Network Building'],
    color: 'secondary',
  },
  {
    icon: 'heroicons:puzzle-piece-20-solid',
    title: 'Joint Ventures',
    description: 'Create strategic partnerships and alliances that multiply your reach and accelerate business growth exponentially.',
    features: ['Partner Matching', 'Deal Structuring', 'Collaboration Strategy'],
    color: 'primary',
  },
  {
    icon: 'heroicons:cog-8-tooth-20-solid',
    title: 'Business Optimization',
    description: 'Streamline operations, eliminate inefficiencies, and maximize profitability through continuous improvement methodologies.',
    features: ['Process Improvement', 'Cost Reduction', 'Efficiency Analysis'],
    color: 'secondary',
  },
]

const colorClasses = {
  primary: {
    bg: 'bg-primary-100',
    icon: 'text-primary-600',
    border: 'group-hover:border-primary-200',
    gradient: 'from-primary-500 to-primary-600',
  },
  secondary: {
    bg: 'bg-secondary-100',
    icon: 'text-secondary-600',
    border: 'group-hover:border-secondary-200',
    gradient: 'from-secondary-500 to-secondary-600',
  },
}
</script>

<template>
  <section id="services" class="py-24 bg-dark-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center mb-16">
        <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
          Services
        </span>
        <h2 class="section-title mb-4">
          How I Can Help You
          <span class="gradient-text">Grow</span>
        </h2>
        <p class="section-subtitle mx-auto">
          Comprehensive consulting services designed to transform your business and accelerate your path to success.
        </p>
      </div>

      <!-- Services Grid -->
      <div class="grid md:grid-cols-2 gap-8">
        <div
          v-for="(service, index) in services"
          :key="service.title"
          class="group card p-8 hover:shadow-2xl"
          :style="{ animationDelay: `${index * 100}ms` }"
        >
          <div class="flex items-start space-x-5">
            <div
              class="flex-shrink-0 w-14 h-14 rounded-2xl flex items-center justify-center transition-all duration-300 group-hover:scale-110"
              :class="colorClasses[service.color].bg"
            >
              <Icon
                :name="service.icon"
                class="w-7 h-7"
                :class="colorClasses[service.color].icon"
              />
            </div>
            <div class="flex-1">
              <h3 class="text-xl font-bold text-dark-900 mb-2 group-hover:text-primary-600 transition-colors">
                {{ service.title }}
              </h3>
              <p class="text-dark-500 mb-4 leading-relaxed">
                {{ service.description }}
              </p>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="feature in service.features"
                  :key="feature"
                  class="px-3 py-1 bg-dark-100 text-dark-600 text-sm rounded-full"
                >
                  {{ feature }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- CTA -->
      <div class="text-center mt-12">
        <NuxtLink to="/services" class="btn-primary">
          View All Services
          <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
        </NuxtLink>
      </div>
    </div>
  </section>
</template>
