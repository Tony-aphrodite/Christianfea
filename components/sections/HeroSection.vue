<script setup lang="ts">
const stats = [
  { value: '15+', label: 'Years Experience' },
  { value: '500+', label: 'Clients Helped' },
  { value: '10x', label: 'Average ROI' },
]
</script>

<template>
  <section class="relative min-h-screen flex items-center overflow-hidden">
    <!-- Background Gradient -->
    <div class="absolute inset-0 bg-gradient-to-br from-dark-900 via-dark-800 to-primary-900"></div>

    <!-- Animated Background Elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute top-1/4 -left-20 w-96 h-96 bg-primary-500/20 rounded-full blur-3xl animate-float"></div>
      <div class="absolute bottom-1/4 -right-20 w-80 h-80 bg-secondary-500/20 rounded-full blur-3xl animate-float" style="animation-delay: -3s;"></div>
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[800px] h-[800px] bg-primary-600/10 rounded-full blur-3xl"></div>
    </div>

    <!-- Grid Pattern -->
    <div class="absolute inset-0 bg-[url('/grid.svg')] bg-center opacity-20"></div>

    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-32 pt-40">
      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <!-- Content -->
        <div class="text-center lg:text-left">
          <div class="inline-flex items-center px-4 py-2 bg-white/10 backdrop-blur-sm rounded-full border border-white/20 mb-8">
            <span class="w-2 h-2 bg-green-400 rounded-full mr-2 animate-pulse"></span>
            <span class="text-sm text-white/80">Available for new clients</span>
          </div>

          <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold text-white leading-tight mb-6">
            Transform Your Business With
            <span class="block mt-2 bg-gradient-to-r from-primary-400 via-primary-300 to-secondary-400 bg-clip-text text-transparent">
              Continuous Improvement
            </span>
          </h1>

          <p class="text-lg sm:text-xl text-dark-300 mb-8 max-w-xl mx-auto lg:mx-0 leading-relaxed">
            I help mission-based entrepreneurs achieve sustainable growth through proven strategies in referral marketing, joint ventures, and business optimization.
          </p>

          <div class="flex flex-col sm:flex-row gap-4 justify-center lg:justify-start mb-12">
            <NuxtLink to="/contact" class="btn-primary text-lg px-8 py-4">
              Schedule Free Consultation
              <Icon name="heroicons:calendar-20-solid" class="w-5 h-5 ml-2" />
            </NuxtLink>
            <NuxtLink to="/services" class="btn-outline text-lg px-8 py-4">
              Explore Services
            </NuxtLink>
          </div>

          <!-- Stats -->
          <div class="grid grid-cols-3 gap-8 pt-8 border-t border-white/10">
            <div v-for="stat in stats" :key="stat.label" class="text-center lg:text-left">
              <div class="text-3xl sm:text-4xl font-bold text-white mb-1">{{ stat.value }}</div>
              <div class="text-sm text-dark-400">{{ stat.label }}</div>
            </div>
          </div>
        </div>

        <!-- Hero Image/Visual -->
        <div class="hidden lg:block relative">
          <div class="relative z-10">
            <!-- Profile Card -->
            <div class="bg-white/10 backdrop-blur-xl rounded-3xl border border-white/20 p-8 shadow-2xl">
              <div class="flex items-center space-x-4 mb-6">
                <div class="w-20 h-20 rounded-2xl overflow-hidden shadow-lg">
                  <img src="/compressed_image.jpg" alt="Anatolii Petrenko" class="w-full h-full object-cover" />
                </div>
                <div>
                  <h3 class="text-xl font-bold text-white">Anatolii Petrenko</h3>
                  <p class="text-primary-300">Business Growth Strategist</p>
                </div>
              </div>

              <div class="space-y-4">
                <div class="flex items-center space-x-3 text-dark-300">
                  <Icon name="heroicons:check-badge-20-solid" class="w-5 h-5 text-green-400" />
                  <span>Certified Business Consultant</span>
                </div>
                <div class="flex items-center space-x-3 text-dark-300">
                  <Icon name="heroicons:check-badge-20-solid" class="w-5 h-5 text-green-400" />
                  <span>Referral Marketing Expert</span>
                </div>
                <div class="flex items-center space-x-3 text-dark-300">
                  <Icon name="heroicons:check-badge-20-solid" class="w-5 h-5 text-green-400" />
                  <span>Joint Venture Specialist</span>
                </div>
              </div>

              <!-- Floating Elements -->
              <div class="absolute -top-4 -right-4 bg-green-500 text-white px-4 py-2 rounded-full text-sm font-semibold shadow-lg">
                Free Q&A Wednesdays
              </div>
            </div>

            <!-- Floating Cards -->
            <div class="absolute -bottom-8 -left-8 bg-white rounded-2xl p-4 shadow-xl animate-float" style="animation-delay: -2s;">
              <div class="flex items-center space-x-3">
                <div class="w-10 h-10 bg-primary-100 rounded-xl flex items-center justify-center">
                  <Icon name="heroicons:chart-bar-20-solid" class="w-5 h-5 text-primary-600" />
                </div>
                <div>
                  <div class="text-sm text-dark-500">Revenue Growth</div>
                  <div class="text-lg font-bold text-dark-900">+247%</div>
                </div>
              </div>
            </div>

            <div class="absolute -top-8 -left-4 bg-white rounded-2xl p-4 shadow-xl animate-float" style="animation-delay: -4s;">
              <div class="flex items-center space-x-3">
                <div class="w-10 h-10 bg-secondary-100 rounded-xl flex items-center justify-center">
                  <Icon name="heroicons:users-20-solid" class="w-5 h-5 text-secondary-600" />
                </div>
                <div>
                  <div class="text-sm text-dark-500">New Referrals</div>
                  <div class="text-lg font-bold text-dark-900">+89/mo</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
      <a href="#services" class="flex flex-col items-center text-white/60 hover:text-white transition-colors">
        <span class="text-sm mb-2">Scroll to explore</span>
        <Icon name="heroicons:chevron-down-20-solid" class="w-6 h-6" />
      </a>
    </div>
  </section>
</template>
