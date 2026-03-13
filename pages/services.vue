<script setup lang="ts">
useSeoMeta({
  title: 'Services | Anatolii Petrenko',
  description: 'Explore my portfolio of AI automation systems and web development projects.',
})

const projects = [
  {
    id: 'ai-automation',
    title: 'AI Automation for Business Growth',
    description: 'I help businesses save time, reduce costs, and increase productivity by building powerful AI automation systems tailored to their needs.',
    details: 'From workflow automation to intelligent chatbots and system integrations, I design solutions that streamline repetitive tasks and improve operational efficiency. Whether you need automated customer support, lead management systems, data processing pipelines, or API integrations, I can build reliable and scalable automation that works 24/7.',
    image: '/serve.png',
    stack: [
      { name: 'PHP', color: 'from-indigo-500 to-indigo-700', letter: 'PHP' },
      { name: 'Node.js', color: 'from-green-500 to-green-700', letter: 'N' },
      { name: 'API', color: 'from-purple-500 to-purple-700', letter: 'API' },
      { name: 'JavaScript', color: 'from-yellow-400 to-yellow-600', letter: 'JS' },
    ],
  },
  {
    id: 'elegant-styles',
    title: 'Elegant Styles — Modern Glamour Collection',
    description: 'Elegant Styles presents a captivating visual campaign designed to highlight modern femininity through glamour and sophistication.',
    details: 'This fashion advertisement blends luxurious aesthetics with contemporary elegance, showcasing statement evening dresses that radiate confidence and charm. The sparkling textures, refined silhouettes, and premium color palette create a high-end visual identity tailored for modern women who embrace style and individuality.\n\nThe balanced composition, soft lighting effects, and glamorous atmosphere enhance the premium feel of the collection, making it ideal for fashion brands seeking a strong and memorable presence across digital platforms, social media campaigns, and online stores.\n\nDesigned to attract attention instantly, this campaign reflects elegance, confidence, and modern luxury in every detail.',
    image: '/clothes.png',
    stack: [
      { name: 'PHP', color: 'from-indigo-500 to-indigo-700', letter: 'PHP' },
      { name: 'Laravel', color: 'from-red-500 to-red-700', letter: 'L' },
      { name: 'MySQL', color: 'from-blue-500 to-blue-700', letter: 'My' },
      { name: 'AWS', color: 'from-orange-400 to-orange-600', letter: 'AWS' },
      { name: 'Vue.js', color: 'from-emerald-500 to-emerald-700', letter: 'V' },
    ],
  },
]
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
          Portfolio
        </span>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-display text-white mb-6">
          My Recent
          <span class="block mt-2 bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Projects
          </span>
        </h1>
        <p class="text-xl text-dark-300 max-w-2xl mx-auto">
          Real-world solutions I've built for businesses — from AI automation to full-stack web platforms.
        </p>
      </div>
    </section>

    <!-- Projects -->
    <section class="py-24 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="space-y-32">
          <div
            v-for="(project, index) in projects"
            :key="project.id"
            :id="project.id"
            class="scroll-mt-24"
          >
            <div
              class="grid lg:grid-cols-2 gap-16 items-center"
            >
              <!-- Image -->
              <div :class="index % 2 === 1 ? 'lg:order-2' : ''">
                <div class="relative group">
                  <!-- Decorative background blob -->
                  <div class="absolute -inset-4 bg-gradient-to-br from-primary-200 to-secondary-200 rounded-[2rem] opacity-40 blur-xl group-hover:opacity-60 transition-opacity duration-500"></div>
                  <!-- Image with styled frame -->
                  <div class="relative rounded-2xl overflow-hidden shadow-2xl ring-1 ring-dark-200/50">
                    <img
                      :src="project.image"
                      :alt="project.title"
                      class="w-full object-cover"
                    />
                  </div>
                </div>
              </div>

              <!-- Content -->
              <div :class="index % 2 === 1 ? 'lg:order-1' : ''">
                <h2 class="text-3xl font-bold text-dark-900 mb-4">
                  {{ project.title }}
                </h2>
                <p class="text-lg text-dark-500 mb-4 leading-relaxed">
                  {{ project.description }}
                </p>
                <p class="text-dark-500 mb-8 leading-relaxed whitespace-pre-line">
                  {{ project.details }}
                </p>

                <!-- Tech Stack -->
                <div class="mb-6">
                  <h4 class="text-sm font-semibold text-dark-400 uppercase tracking-wider mb-4">Tech Stack</h4>
                  <div class="flex flex-wrap gap-3">
                    <div
                      v-for="tech in project.stack"
                      :key="tech.name"
                      class="group/tech relative"
                    >
                      <div
                        class="w-14 h-14 rounded-xl bg-gradient-to-br shadow-lg flex items-center justify-center text-white font-bold text-sm transform transition-all duration-300 hover:scale-110 hover:shadow-xl hover:-translate-y-1 cursor-default"
                        :class="tech.color"
                      >
                        {{ tech.letter }}
                      </div>
                      <!-- Tooltip -->
                      <div class="absolute -top-8 left-1/2 -translate-x-1/2 bg-dark-900 text-white text-xs px-2 py-1 rounded opacity-0 group-hover/tech:opacity-100 transition-opacity whitespace-nowrap pointer-events-none">
                        {{ tech.name }}
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
