<script setup lang="ts">
const currentYear = new Date().getFullYear()

const footerLinks = {
  services: [
    { name: 'Business Consulting', href: '/services#consulting' },
    { name: 'Growth Strategy', href: '/services#strategy' },
    { name: 'Referral Marketing', href: '/services#referral' },
    { name: 'Joint Ventures', href: '/services#ventures' },
  ],
  resources: [
    { name: 'Blog', href: '/blog' },
    { name: 'Free Resources', href: '/resources' },
    { name: 'JV Wealth Report', href: '/jv-report' },
    { name: 'AI Daily Catalyst', href: '/ai-catalyst' },
  ],
  company: [
    { name: 'About', href: '/about' },
    { name: 'Contact', href: '/contact' },
    { name: 'Schedule Call', href: '/contact#schedule' },
    { name: 'Client Portal', href: '/client-portal' },
  ],
}

const socialLinks = [
  { name: 'LinkedIn', icon: 'mdi:linkedin', href: '#' },
  { name: 'Twitter', icon: 'mdi:twitter', href: '#' },
  { name: 'YouTube', icon: 'mdi:youtube', href: '#' },
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
            Helping mission-based entrepreneurs transform themselves and the people they influence through continuous improvement strategies.
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
          <h3 class="text-sm font-semibold uppercase tracking-wider text-dark-400 mb-4">Services</h3>
          <ul class="space-y-3">
            <li v-for="link in footerLinks.services" :key="link.name">
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
          <h3 class="text-sm font-semibold uppercase tracking-wider text-dark-400 mb-4">Company</h3>
          <ul class="space-y-3">
            <li v-for="link in footerLinks.company" :key="link.name">
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
