<template>
  <section class="py-24 bg-gradient-to-br from-primary-600 via-primary-700 to-primary-800 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0">
      <div class="absolute top-0 right-0 w-96 h-96 bg-white/5 rounded-full blur-3xl"></div>
      <div class="absolute bottom-0 left-0 w-80 h-80 bg-secondary-500/10 rounded-full blur-3xl"></div>
    </div>

    <div class="relative max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <h2 class="text-3xl sm:text-4xl lg:text-5xl font-bold font-display text-white mb-6">
        Ready to Transform Your Business?
      </h2>
      <p class="text-xl text-primary-100 mb-10 max-w-2xl mx-auto leading-relaxed">
        Take the first step towards sustainable growth. Schedule a free consultation and discover how we can work together to achieve your goals.
      </p>

      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <NuxtLink
          to="/contact"
          class="inline-flex items-center justify-center px-8 py-4 text-lg font-semibold text-primary-700 bg-white rounded-xl shadow-xl hover:shadow-2xl hover:-translate-y-0.5 transition-all duration-300"
        >
          Schedule Free Consultation
          <Icon name="heroicons:calendar-20-solid" class="w-5 h-5 ml-2" />
        </NuxtLink>
        <NuxtLink
          to="/services"
          class="inline-flex items-center justify-center px-8 py-4 text-lg font-semibold text-white border-2 border-white/30 rounded-xl hover:bg-white/10 hover:border-white/50 transition-all duration-300"
        >
          View Services
        </NuxtLink>
      </div>

      <!-- Trust Indicators -->
      <div class="mt-12 pt-12 border-t border-white/20">
        <div class="flex flex-wrap justify-center items-center gap-8 text-primary-200">
          <div class="flex items-center space-x-2">
            <Icon name="heroicons:check-badge-20-solid" class="w-5 h-5" />
            <span>No Commitment Required</span>
          </div>
          <div class="flex items-center space-x-2">
            <Icon name="heroicons:check-badge-20-solid" class="w-5 h-5" />
            <span>100% Confidential</span>
          </div>
          <div class="flex items-center space-x-2">
            <Icon name="heroicons:check-badge-20-solid" class="w-5 h-5" />
            <span>Actionable Insights</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
