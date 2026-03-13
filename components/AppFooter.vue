<script setup lang="ts">
const currentYear = new Date().getFullYear()

const footerLinks = {
  portfolio: [
    { name: 'AI Automation', href: '/services#ai-automation' },
    { name: 'E-Commerce Platform', href: '/services#elegant-styles' },
    { name: 'CRM Platform', href: '/services#ai-crm' },
    { name: 'AI Chatbot System', href: '/services#ai-chatbot' },
  ],
  resources: [
    { name: 'Products', href: '/blog' },
    { name: 'About Me', href: '/about' },
    { name: 'My Experience', href: '/about#experience' },
  ],
  connect: [
    { name: 'Contact', href: '/contact' },
    { name: 'Send Message', href: '/contact#schedule' },
  ],
}

const socialLinks = [
  { name: 'GitHub', icon: 'mdi:github', href: '#' },
  { name: 'LinkedIn', icon: 'mdi:linkedin', href: '#' },
  { name: 'Twitter', icon: 'mdi:twitter', href: '#' },
]
</script>

<template>
  <footer class="bg-dark-900 text-white">
    <!-- Main Footer -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-12">
        <!-- Brand Column -->
        <div class="lg:col-span-2">
          <NuxtLink to="/" class="flex items-center space-x-3 mb-6">
            <div class="w-10 h-10 bg-gradient-to-br from-primary-400 to-primary-600 rounded-xl flex items-center justify-center">
              <span class="text-white font-bold text-xl">A</span>
            </div>
            <div>
              <span class="text-xl font-bold text-white">Anatolii</span>
              <span class="text-xl font-bold text-primary-400">Petrenko</span>
            </div>
          </NuxtLink>
          <p class="text-dark-300 mb-6 max-w-sm leading-relaxed">
            AI Full-Stack Developer specializing in building scalable web & mobile applications with modern AI technologies.
          </p>
          <div class="flex space-x-4">
            <a
              v-for="social in socialLinks"
              :key="social.name"
              :href="social.href"
              class="w-10 h-10 bg-dark-800 rounded-lg flex items-center justify-center text-dark-400 hover:bg-primary-600 hover:text-white transition-all duration-300"
              :aria-label="social.name"
            >
              <Icon :name="social.icon" class="w-5 h-5" />
            </a>
          </div>
        </div>

        <!-- Services Links -->
        <div>
          <h3 class="text-sm font-semibold uppercase tracking-wider text-dark-400 mb-4">Portfolio</h3>
          <ul class="space-y-3">
            <li v-for="link in footerLinks.portfolio" :key="link.name">
              <NuxtLink
                :to="link.href"
                class="text-dark-300 hover:text-primary-400 transition-colors"
              >
                {{ link.name }}
              </NuxtLink>
            </li>
          </ul>
        </div>

        <!-- Resources Links -->
        <div>
          <h3 class="text-sm font-semibold uppercase tracking-wider text-dark-400 mb-4">Resources</h3>
          <ul class="space-y-3">
            <li v-for="link in footerLinks.resources" :key="link.name">
              <NuxtLink
                :to="link.href"
                class="text-dark-300 hover:text-primary-400 transition-colors"
              >
                {{ link.name }}
              </NuxtLink>
            </li>
          </ul>
        </div>

        <!-- Company Links -->
        <div>
          <h3 class="text-sm font-semibold uppercase tracking-wider text-dark-400 mb-4">Connect</h3>
          <ul class="space-y-3">
            <li v-for="link in footerLinks.connect" :key="link.name">
              <NuxtLink
                :to="link.href"
                class="text-dark-300 hover:text-primary-400 transition-colors"
              >
                {{ link.name }}
              </NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Bottom Bar -->
    <div class="border-t border-dark-800">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
        <div class="flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0">
          <p class="text-dark-400 text-sm">
            &copy; {{ currentYear }} Anatolii Petrenko. All rights reserved.
          </p>
          <div class="flex space-x-6">
            <NuxtLink to="/privacy" class="text-dark-400 text-sm hover:text-primary-400 transition-colors">
              Privacy Policy
            </NuxtLink>
            <NuxtLink to="/terms" class="text-dark-400 text-sm hover:text-primary-400 transition-colors">
              Terms of Service
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>
