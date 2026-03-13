<script setup lang="ts">
const testimonials = [
  {
    content: "Anatolii built our e-commerce platform from scratch and it's been running smoothly for over a year now. He understood our requirements quickly, communicated clearly throughout the process, and delivered on time. The admin panel he built saves us hours every week.",
    author: "David Park",
    role: "Founder, StyleVault",
    avatar: "DP",
    rating: 5,
  },
  {
    content: "We needed an AI chatbot integrated with WhatsApp for customer support. Anatolii not only delivered exactly what we asked for, but also suggested improvements we hadn't thought of. Response time dropped from hours to seconds, and our support team can now focus on complex issues.",
    author: "Laura Kim",
    role: "Operations Manager, FreshDesk Co.",
    avatar: "LK",
    rating: 5,
  },
  {
    content: "Anatolii helped us migrate our legacy CRM to a modern stack with AI-powered lead scoring. The transition was smooth, and the new system is significantly faster. He was patient with our team during onboarding and always available when we had questions.",
    author: "James Mitchell",
    role: "CTO, GrowthPath Inc.",
    avatar: "JM",
    rating: 5,
  },
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
          What Clients
          <span class="bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Say
          </span>
        </h2>
        <p class="text-lg text-dark-300 max-w-2xl mx-auto">
          Feedback from businesses I've worked with on real projects.
        </p>
      </div>

      <!-- Testimonials Grid -->
      <div class="grid md:grid-cols-3 gap-8">
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
    </div>
  </section>
</template>
