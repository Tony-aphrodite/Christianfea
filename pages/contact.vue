<script setup lang="ts">
useSeoMeta({
  title: 'Contact | Anatolii Petrenko',
  description: 'Get in touch with Anatolii Petrenko. Schedule a free consultation or join the Wednesday Q&A sessions.',
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
  'Business Growth Strategy',
  'Referral Marketing',
  'Joint Ventures',
  'Business Optimization',
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
    description: 'For general inquiries',
    value: 'contact@anatoliipetrenko.com',
    href: 'mailto:contact@anatoliipetrenko.com',
    action: 'Send Email',
  },
  {
    icon: 'heroicons:calendar-20-solid',
    title: 'Schedule a Call',
    description: 'Book a free consultation',
    value: '30-minute discovery call',
    href: '#schedule',
    action: 'Book Now',
  },
  {
    icon: 'heroicons:video-camera-20-solid',
    title: 'Wednesday Q&A',
    description: 'Free weekly sessions',
    value: 'Every Wednesday @ 4PM PST',
    href: '#schedule',
    action: 'Join Session',
  },
]

const faqs = [
  {
    question: 'How does the free consultation work?',
    answer: 'The free consultation is a 30-minute discovery call where we discuss your business challenges and goals. I\'ll provide initial insights and we\'ll determine if working together would be a good fit.',
  },
  {
    question: 'What industries do you work with?',
    answer: 'I work with mission-based entrepreneurs across various industries. The common thread is a commitment to growth and a desire to make a positive impact through their business.',
  },
  {
    question: 'How long does a typical engagement last?',
    answer: 'Engagements vary based on your needs. Some clients work with me on specific projects, while others engage in ongoing consulting relationships. We\'ll discuss the best approach during our initial consultation.',
  },
  {
    question: 'What are the Wednesday Q&A sessions?',
    answer: 'Every Wednesday at 4PM PST, I host free internet marketing Q&A sessions. These are open discussions where you can ask questions about marketing, business growth, and strategy—no sales pitch, just valuable insights.',
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
          Ready to transform your business? I'd love to hear from you. Choose the best way to connect below.
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

          <!-- Schedule -->
          <div>
            <h2 class="section-title mb-4">
              Book a <span class="gradient-text">Call</span>
            </h2>
            <p class="text-lg text-dark-500 mb-8">
              Schedule a free 30-minute discovery call to discuss your business goals.
            </p>

            <!-- Calendar Placeholder -->
            <div class="bg-white rounded-3xl p-8 shadow-xl">
              <div class="aspect-video bg-dark-100 rounded-2xl flex items-center justify-center mb-6">
                <div class="text-center">
                  <Icon name="heroicons:calendar-days-20-solid" class="w-16 h-16 text-dark-300 mx-auto mb-4" />
                  <p class="text-dark-500">Calendar integration would go here</p>
                  <p class="text-sm text-dark-400">(e.g., Calendly, Cal.com)</p>
                </div>
              </div>

              <div class="bg-primary-50 rounded-xl p-6">
                <h3 class="font-bold text-dark-900 mb-2">Free Wednesday Q&A Sessions</h3>
                <p class="text-dark-600 text-sm mb-4">
                  Join me every Wednesday at 4PM PST for free internet marketing Q&A sessions. No sales pitch, just valuable insights and answers to your questions.
                </p>
                <div class="flex items-center text-primary-600">
                  <Icon name="heroicons:clock-20-solid" class="w-5 h-5 mr-2" />
                  <span class="font-medium">Wednesdays @ 4:00 PM PST</span>
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
