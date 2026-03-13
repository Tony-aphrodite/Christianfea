<script setup lang="ts">
const formData = reactive({
  name: '',
  email: '',
  phone: '',
  message: '',
})

const isSubmitting = ref(false)
const isSubmitted = ref(false)

async function handleSubmit() {
  isSubmitting.value = true
  // Simulate API call
  await new Promise(resolve => setTimeout(resolve, 1500))
  isSubmitting.value = false
  isSubmitted.value = true
}

const contactInfo = [
  {
    icon: 'heroicons:envelope-20-solid',
    label: 'Email',
    value: 'contact@anatoliipetrenko.com',
    href: 'mailto:contact@anatoliipetrenko.com',
  },
  {
    icon: 'heroicons:calendar-20-solid',
    label: 'Free Q&A Session',
    value: 'Wednesdays @ 4PM PST',
    href: '/contact#schedule',
  },
  {
    icon: 'heroicons:map-pin-20-solid',
    label: 'Location',
    value: 'Available Worldwide',
    href: null,
  },
]
</script>

<template>
  <section id="contact" class="py-24 bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid lg:grid-cols-2 gap-16">
        <!-- Content Side -->
        <div>
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            Get In Touch
          </span>
          <h2 class="section-title mb-6">
            Let's Start Your
            <span class="gradient-text">Growth Journey</span>
          </h2>
          <p class="text-lg text-dark-500 mb-8 leading-relaxed">
            Ready to transform your business? Schedule a free consultation to discuss your goals and discover how we can work together to achieve extraordinary results.
          </p>

          <!-- Contact Info -->
          <div class="space-y-6 mb-8">
            <div
              v-for="info in contactInfo"
              :key="info.label"
              class="flex items-center space-x-4"
            >
              <div class="w-12 h-12 bg-primary-100 rounded-xl flex items-center justify-center">
                <Icon :name="info.icon" class="w-6 h-6 text-primary-600" />
              </div>
              <div>
                <div class="text-sm text-dark-400">{{ info.label }}</div>
                <component
                  :is="info.href ? 'a' : 'span'"
                  :href="info.href"
                  class="font-semibold text-dark-900"
                  :class="info.href ? 'hover:text-primary-600 transition-colors' : ''"
                >
                  {{ info.value }}
                </component>
              </div>
            </div>
          </div>

          <!-- Quick Action Card -->
          <div class="bg-gradient-to-br from-primary-500 to-primary-700 rounded-2xl p-8 text-white">
            <h3 class="text-xl font-bold mb-2">Free Wednesday Q&A Sessions</h3>
            <p class="text-primary-100 mb-4">
              Join me every Wednesday at 4PM PST for free internet marketing Q&A sessions. No sales pitch, just valuable insights.
            </p>
            <NuxtLink to="/contact#schedule" class="inline-flex items-center font-semibold hover:underline">
              Reserve Your Spot
              <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
            </NuxtLink>
          </div>
        </div>

        <!-- Form Side -->
        <div class="bg-dark-50 rounded-3xl p-8 lg:p-10">
          <Transition
            mode="out-in"
            enter-active-class="transition-all duration-300 ease-out"
            enter-from-class="opacity-0 scale-95"
            enter-to-class="opacity-100 scale-100"
            leave-active-class="transition-all duration-200 ease-in"
            leave-from-class="opacity-100 scale-100"
            leave-to-class="opacity-0 scale-95"
          >
            <!-- Success State -->
            <div v-if="isSubmitted" class="text-center py-12">
              <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-6">
                <Icon name="heroicons:check-20-solid" class="w-8 h-8 text-green-600" />
              </div>
              <h3 class="text-2xl font-bold text-dark-900 mb-2">Message Sent!</h3>
              <p class="text-dark-500 mb-6">
                Thank you for reaching out. I'll get back to you within 24 hours.
              </p>
              <button
                class="btn-secondary"
                @click="isSubmitted = false"
              >
                Send Another Message
              </button>
            </div>

            <!-- Form -->
            <form v-else @submit.prevent="handleSubmit" class="space-y-6">
              <div>
                <label for="name" class="block text-sm font-medium text-dark-700 mb-2">
                  Full Name
                </label>
                <input
                  id="name"
                  v-model="formData.name"
                  type="text"
                  required
                  placeholder="John Smith"
                  class="w-full px-4 py-3 bg-white border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                />
              </div>

              <div>
                <label for="email" class="block text-sm font-medium text-dark-700 mb-2">
                  Email Address
                </label>
                <input
                  id="email"
                  v-model="formData.email"
                  type="email"
                  required
                  placeholder="john@example.com"
                  class="w-full px-4 py-3 bg-white border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                />
              </div>

              <div>
                <label for="phone" class="block text-sm font-medium text-dark-700 mb-2">
                  Phone Number (Optional)
                </label>
                <input
                  id="phone"
                  v-model="formData.phone"
                  type="tel"
                  placeholder="+1 (555) 000-0000"
                  class="w-full px-4 py-3 bg-white border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                />
              </div>

              <div>
                <label for="message" class="block text-sm font-medium text-dark-700 mb-2">
                  How Can I Help You?
                </label>
                <textarea
                  id="message"
                  v-model="formData.message"
                  rows="4"
                  required
                  placeholder="Tell me about your business goals and challenges..."
                  class="w-full px-4 py-3 bg-white border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none resize-none"
                ></textarea>
              </div>

              <button
                type="submit"
                class="btn-primary w-full"
                :disabled="isSubmitting"
              >
                <template v-if="isSubmitting">
                  <Icon name="heroicons:arrow-path-20-solid" class="w-5 h-5 mr-2 animate-spin" />
                  Sending...
                </template>
                <template v-else>
                  Send Message
                  <Icon name="heroicons:paper-airplane-20-solid" class="w-5 h-5 ml-2" />
                </template>
              </button>

              <p class="text-sm text-dark-400 text-center">
                By submitting this form, you agree to our
                <NuxtLink to="/privacy" class="text-primary-600 hover:underline">Privacy Policy</NuxtLink>.
              </p>
            </form>
          </Transition>
        </div>
      </div>
    </div>
  </section>
</template>
