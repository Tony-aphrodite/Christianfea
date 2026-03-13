<script setup lang="ts">
useSeoMeta({
  title: 'Contact | Anatolii Petrenko',
  description: 'Get in touch with Anatolii Petrenko for web development, mobile apps, and AI automation projects.',
})

const formData = reactive({
  name: '',
  email: '',
  phone: '',
  service: '',
  message: '',
})

const isSubmitting = ref(false)
const isSubmitted = ref(false)

const services = [
  'Full-Stack Web Development',
  'Mobile App Development',
  'AI Automation & Chatbots',
  'API Integration',
  'General Inquiry',
]

async function handleSubmit() {
  isSubmitting.value = true
  await new Promise(resolve => setTimeout(resolve, 1500))
  isSubmitting.value = false
  isSubmitted.value = true
}

const contactMethods = [
  {
    icon: 'heroicons:envelope-20-solid',
    title: 'Email',
    description: 'For project inquiries',
    value: 'contact@anatoliipetrenko.com',
    href: 'mailto:contact@anatoliipetrenko.com',
    action: 'Send Email',
  },
  {
    icon: 'heroicons:code-bracket-20-solid',
    title: 'GitHub',
    description: 'Check out my code',
    value: 'Open source projects',
    href: '#',
    action: 'View GitHub',
  },
  {
    icon: 'heroicons:briefcase-20-solid',
    title: 'LinkedIn',
    description: 'Professional network',
    value: 'Connect with me',
    href: '#',
    action: 'View Profile',
  },
]

const faqs = [
  {
    question: 'What services do you offer?',
    answer: 'I specialize in full-stack web development, mobile app development, AI-powered automation systems, and API integrations. Whether you need a complete platform from scratch, an AI chatbot, or workflow automation — I can help.',
  },
  {
    question: 'What is your tech stack?',
    answer: 'I work with React, Next.js, Vue.js, Node.js, Python, FastAPI, PHP, Laravel, PostgreSQL, Firebase, Docker, and AWS. For AI projects, I integrate OpenAI, Claude API, and custom NLP models.',
  },
  {
    question: 'How long does a typical project take?',
    answer: 'It depends on the scope. A landing page or simple web app can be delivered in 1-2 weeks. Full-stack platforms or AI systems typically take 4-8 weeks. I\'ll provide a clear timeline after understanding your requirements.',
  },
  {
    question: 'Do you work with startups or only established businesses?',
    answer: 'I work with both. For startups, I help build MVPs quickly and cost-effectively. For established businesses, I focus on scaling existing systems, adding AI automation, and improving performance.',
  },
]

const openFaq = ref<number | null>(null)

function toggleFaq(index: number) {
  openFaq.value = openFaq.value === index ? null : index
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
          Contact
        </span>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-display text-white mb-6">
          Let's Start a
          <span class="bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Conversation
          </span>
        </h1>
        <p class="text-xl text-dark-300 max-w-2xl mx-auto">
          Have a project in mind? I'd love to hear about it. Choose the best way to connect below.
        </p>
      </div>
    </section>

    <!-- Contact Methods -->
    <section class="py-16 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid md:grid-cols-3 gap-8">
          <div
            v-for="method in contactMethods"
            :key="method.title"
            class="card p-8 text-center"
          >
            <div class="w-16 h-16 bg-primary-100 rounded-2xl flex items-center justify-center mx-auto mb-4">
              <Icon :name="method.icon" class="w-8 h-8 text-primary-600" />
            </div>
            <h3 class="text-xl font-bold text-dark-900 mb-2">{{ method.title }}</h3>
            <p class="text-dark-400 text-sm mb-2">{{ method.description }}</p>
            <p class="text-dark-700 font-medium mb-4">{{ method.value }}</p>
            <a
              :href="method.href"
              class="text-primary-600 font-semibold hover:text-primary-700 transition-colors inline-flex items-center"
            >
              {{ method.action }}
              <Icon name="heroicons:arrow-right-20-solid" class="w-4 h-4 ml-1" />
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Form & Schedule -->
    <section id="schedule" class="py-24 bg-dark-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid lg:grid-cols-2 gap-16">
          <!-- Form -->
          <div>
            <h2 class="section-title mb-4">
              Send a <span class="gradient-text">Message</span>
            </h2>
            <p class="text-lg text-dark-500 mb-8">
              Fill out the form below and I'll get back to you within 24 hours.
            </p>

            <div class="bg-white rounded-3xl p-8 shadow-xl">
              <Transition
                mode="out-in"
                enter-active-class="transition-all duration-300 ease-out"
                enter-from-class="opacity-0 scale-95"
                enter-to-class="opacity-100 scale-100"
                leave-active-class="transition-all duration-200 ease-in"
                leave-from-class="opacity-100 scale-100"
                leave-to-class="opacity-0 scale-95"
              >
                <div v-if="isSubmitted" class="text-center py-12">
                  <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-6">
                    <Icon name="heroicons:check-20-solid" class="w-8 h-8 text-green-600" />
                  </div>
                  <h3 class="text-2xl font-bold text-dark-900 mb-2">Message Sent!</h3>
                  <p class="text-dark-500 mb-6">
                    Thank you for reaching out. I'll get back to you within 24 hours.
                  </p>
                  <button class="btn-secondary" @click="isSubmitted = false">
                    Send Another Message
                  </button>
                </div>

                <form v-else @submit.prevent="handleSubmit" class="space-y-6">
                  <div class="grid sm:grid-cols-2 gap-6">
                    <div>
                      <label for="name" class="block text-sm font-medium text-dark-700 mb-2">
                        Full Name *
                      </label>
                      <input
                        id="name"
                        v-model="formData.name"
                        type="text"
                        required
                        placeholder="John Smith"
                        class="w-full px-4 py-3 bg-dark-50 border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                      />
                    </div>
                    <div>
                      <label for="email" class="block text-sm font-medium text-dark-700 mb-2">
                        Email Address *
                      </label>
                      <input
                        id="email"
                        v-model="formData.email"
                        type="email"
                        required
                        placeholder="john@example.com"
                        class="w-full px-4 py-3 bg-dark-50 border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                      />
                    </div>
                  </div>

                  <div class="grid sm:grid-cols-2 gap-6">
                    <div>
                      <label for="phone" class="block text-sm font-medium text-dark-700 mb-2">
                        Phone Number
                      </label>
                      <input
                        id="phone"
                        v-model="formData.phone"
                        type="tel"
                        placeholder="+1 (555) 000-0000"
                        class="w-full px-4 py-3 bg-dark-50 border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                      />
                    </div>
                    <div>
                      <label for="service" class="block text-sm font-medium text-dark-700 mb-2">
                        Service Interest
                      </label>
                      <select
                        id="service"
                        v-model="formData.service"
                        class="w-full px-4 py-3 bg-dark-50 border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
                      >
                        <option value="">Select a service</option>
                        <option v-for="service in services" :key="service" :value="service">
                          {{ service }}
                        </option>
                      </select>
                    </div>
                  </div>

                  <div>
                    <label for="message" class="block text-sm font-medium text-dark-700 mb-2">
                      Your Message *
                    </label>
                    <textarea
                      id="message"
                      v-model="formData.message"
                      rows="5"
                      required
                      placeholder="Tell me about your business goals and challenges..."
                      class="w-full px-4 py-3 bg-dark-50 border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none resize-none"
                    ></textarea>
                  </div>

                  <button type="submit" class="btn-primary w-full" :disabled="isSubmitting">
                    <template v-if="isSubmitting">
                      <Icon name="heroicons:arrow-path-20-solid" class="w-5 h-5 mr-2 animate-spin" />
                      Sending...
                    </template>
                    <template v-else>
                      Send Message
                      <Icon name="heroicons:paper-airplane-20-solid" class="w-5 h-5 ml-2" />
                    </template>
                  </button>
                </form>
              </Transition>
            </div>
          </div>

          <!-- What I Can Build -->
          <div>
            <h2 class="section-title mb-4">
              What I Can <span class="gradient-text">Build</span>
            </h2>
            <p class="text-lg text-dark-500 mb-8">
              From idea to deployment — here's what I can help you with.
            </p>

            <div class="bg-white rounded-3xl p-8 shadow-xl space-y-6">
              <div class="flex items-start space-x-4">
                <div class="w-12 h-12 bg-primary-100 rounded-xl flex items-center justify-center flex-shrink-0">
                  <Icon name="heroicons:globe-alt-20-solid" class="w-6 h-6 text-primary-600" />
                </div>
                <div>
                  <h3 class="font-bold text-dark-900 mb-1">Web Applications</h3>
                  <p class="text-dark-500 text-sm">Full-stack platforms, SaaS products, e-commerce, dashboards, and admin panels.</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="w-12 h-12 bg-secondary-100 rounded-xl flex items-center justify-center flex-shrink-0">
                  <Icon name="heroicons:device-phone-mobile-20-solid" class="w-6 h-6 text-secondary-600" />
                </div>
                <div>
                  <h3 class="font-bold text-dark-900 mb-1">Mobile Apps</h3>
                  <p class="text-dark-500 text-sm">Cross-platform iOS & Android apps with React Native and Flutter.</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="w-12 h-12 bg-orange-100 rounded-xl flex items-center justify-center flex-shrink-0">
                  <Icon name="heroicons:cpu-chip-20-solid" class="w-6 h-6 text-orange-600" />
                </div>
                <div>
                  <h3 class="font-bold text-dark-900 mb-1">AI & Automation</h3>
                  <p class="text-dark-500 text-sm">AI chatbots, workflow automation, GPT integrations, and intelligent data processing.</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="w-12 h-12 bg-green-100 rounded-xl flex items-center justify-center flex-shrink-0">
                  <Icon name="heroicons:arrow-path-20-solid" class="w-6 h-6 text-green-600" />
                </div>
                <div>
                  <h3 class="font-bold text-dark-900 mb-1">API & Integrations</h3>
                  <p class="text-dark-500 text-sm">RESTful APIs, third-party integrations, payment gateways, and CRM connections.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ -->
    <section class="py-24 bg-white">
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-12">
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            FAQ
          </span>
          <h2 class="section-title">
            Frequently Asked <span class="gradient-text">Questions</span>
          </h2>
        </div>

        <div class="space-y-4">
          <div
            v-for="(faq, index) in faqs"
            :key="index"
            class="border border-dark-200 rounded-xl overflow-hidden"
          >
            <button
              class="w-full px-6 py-4 flex items-center justify-between text-left hover:bg-dark-50 transition-colors"
              @click="toggleFaq(index)"
            >
              <span class="font-semibold text-dark-900">{{ faq.question }}</span>
              <Icon
                name="heroicons:chevron-down-20-solid"
                class="w-5 h-5 text-dark-400 transition-transform duration-200"
                :class="openFaq === index ? 'rotate-180' : ''"
              />
            </button>
            <Transition
              enter-active-class="transition-all duration-200 ease-out"
              enter-from-class="opacity-0 max-h-0"
              enter-to-class="opacity-100 max-h-96"
              leave-active-class="transition-all duration-150 ease-in"
              leave-from-class="opacity-100 max-h-96"
              leave-to-class="opacity-0 max-h-0"
            >
              <div v-if="openFaq === index" class="px-6 pb-4">
                <p class="text-dark-500">{{ faq.answer }}</p>
              </div>
            </Transition>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
