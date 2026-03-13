<script setup lang="ts">
const testimonials = [
  {
    content: "Working with Anatolii transformed our referral strategy completely. We went from struggling to get word-of-mouth leads to having a systematic approach that generates consistent, high-quality referrals every month.",
    author: "Sarah Johnson",
    role: "CEO, Growth Marketing Co.",
    avatar: "SJ",
    rating: 5,
  },
  {
    content: "Anatolii's joint venture expertise helped us form partnerships that would have taken years to develop on our own. Our revenue increased by 300% in the first year of implementing his strategies.",
    author: "Michael Chen",
    role: "Founder, TechScale Solutions",
    avatar: "MC",
    rating: 5,
  },
  {
    content: "The continuous improvement framework Anatolii introduced to our business has become the backbone of our operations. We're more efficient, profitable, and our team is more aligned than ever.",
    author: "Emily Rodriguez",
    role: "Director, Innovate Partners",
    avatar: "ER",
    rating: 5,
  },
]

const brands = [
  'Company A',
  'Company B',
  'Company C',
  'Company D',
  'Company E',
]
</script>

<template>
  <section id="testimonials" class="py-24 bg-gradient-to-br from-dark-900 via-dark-800 to-primary-900 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0">
      <div class="absolute top-0 left-1/4 w-96 h-96 bg-primary-500/10 rounded-full blur-3xl"></div>
      <div class="absolute bottom-0 right-1/4 w-80 h-80 bg-secondary-500/10 rounded-full blur-3xl"></div>
    </div>

    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center mb-16">
        <span class="inline-block px-4 py-1.5 bg-white/10 text-primary-300 text-sm font-semibold rounded-full mb-4">
          Testimonials
        </span>
        <h2 class="text-4xl md:text-5xl font-bold font-display text-white tracking-tight mb-4">
          Trusted by
          <span class="bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Industry Leaders
          </span>
        </h2>
        <p class="text-lg text-dark-300 max-w-2xl mx-auto">
          See what entrepreneurs and business owners have to say about working with me.
        </p>
      </div>

      <!-- Testimonials Grid -->
      <div class="grid md:grid-cols-3 gap-8 mb-16">
        <div
          v-for="(testimonial, index) in testimonials"
          :key="index"
          class="bg-white/5 backdrop-blur-sm rounded-2xl p-8 border border-white/10 hover:border-primary-500/50 transition-all duration-300 hover:-translate-y-1"
        >
          <!-- Rating -->
          <div class="flex space-x-1 mb-4">
            <Icon
              v-for="star in testimonial.rating"
              :key="star"
              name="heroicons:star-solid"
              class="w-5 h-5 text-yellow-400"
            />
          </div>

          <!-- Content -->
          <p class="text-dark-200 leading-relaxed mb-6">
            "{{ testimonial.content }}"
          </p>

          <!-- Author -->
          <div class="flex items-center space-x-4">
            <div class="w-12 h-12 bg-gradient-to-br from-primary-400 to-primary-600 rounded-full flex items-center justify-center text-white font-semibold">
              {{ testimonial.avatar }}
            </div>
            <div>
              <div class="font-semibold text-white">{{ testimonial.author }}</div>
              <div class="text-sm text-dark-400">{{ testimonial.role }}</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Trusted By -->
      <div class="text-center">
        <p class="text-dark-400 text-sm uppercase tracking-wider mb-8">Trusted by businesses worldwide</p>
        <div class="flex flex-wrap justify-center items-center gap-8 md:gap-16">
          <div
            v-for="brand in brands"
            :key="brand"
            class="text-dark-500 font-semibold text-lg opacity-50 hover:opacity-100 transition-opacity"
          >
            {{ brand }}
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
