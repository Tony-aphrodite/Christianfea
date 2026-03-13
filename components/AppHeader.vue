<script setup lang="ts">
const isMenuOpen = ref(false)
const isScrolled = ref(false)

const navLinks = [
  { name: 'Home', href: '/' },
  { name: 'Services', href: '/services' },
  { name: 'About', href: '/about' },
  { name: 'Products', href: '/blog' },
  { name: 'Contact', href: '/contact' },
]

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

function handleScroll() {
  isScrolled.value = window.scrollY > 20
}

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
}

function closeMenu() {
  isMenuOpen.value = false
}
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="isScrolled ? 'bg-white/95 backdrop-blur-lg shadow-lg shadow-dark-900/5' : 'bg-transparent'"
  >
    <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-20">
        <!-- Logo -->
        <NuxtLink to="/" class="flex items-center space-x-3 group" @click="closeMenu">
          <div class="w-10 h-10 bg-gradient-to-br from-primary-500 to-primary-700 rounded-xl flex items-center justify-center shadow-lg shadow-primary-500/30 group-hover:shadow-xl group-hover:shadow-primary-500/40 transition-all duration-300">
            <span class="text-white font-bold text-xl">A</span>
          </div>
          <div class="hidden sm:block">
            <span class="text-xl font-bold text-dark-900">Anatolii</span>
            <span class="text-xl font-bold text-primary-600">Petrenko</span>
          </div>
        </NuxtLink>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-1">
          <NuxtLink
            v-for="link in navLinks"
            :key="link.name"
            :to="link.href"
            class="px-4 py-2 text-dark-600 font-medium rounded-lg hover:text-primary-600 hover:bg-primary-50 transition-all duration-200"
            active-class="text-primary-600 bg-primary-50"
          >
            {{ link.name }}
          </NuxtLink>
        </div>

        <!-- Mobile Menu Button -->
        <button
          class="md:hidden p-2 rounded-lg hover:bg-dark-100 transition-colors"
          @click="toggleMenu"
          aria-label="Toggle menu"
        >
          <Icon
            :name="isMenuOpen ? 'heroicons:x-mark-20-solid' : 'heroicons:bars-3-20-solid'"
            class="w-6 h-6 text-dark-700"
          />
        </button>
      </div>

      <!-- Mobile Menu -->
      <Transition
        enter-active-class="transition-all duration-300 ease-out"
        enter-from-class="opacity-0 -translate-y-4"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition-all duration-200 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-4"
      >
        <div
          v-if="isMenuOpen"
          class="md:hidden absolute top-full left-0 right-0 bg-white shadow-xl border-t border-dark-100"
        >
          <div class="px-4 py-6 space-y-2">
            <NuxtLink
              v-for="link in navLinks"
              :key="link.name"
              :to="link.href"
              class="block px-4 py-3 text-dark-700 font-medium rounded-lg hover:bg-primary-50 hover:text-primary-600 transition-colors"
              active-class="bg-primary-50 text-primary-600"
              @click="closeMenu"
            >
              {{ link.name }}
            </NuxtLink>
          </div>
        </div>
      </Transition>
    </nav>
  </header>
</template>
