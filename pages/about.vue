<script setup lang="ts">
useSeoMeta({
  title: 'About | Anatolii Petrenko',
  description: 'Learn about Anatolii Petrenko, a business growth strategist helping mission-based entrepreneurs transform their businesses through continuous improvement.',
})

const timeline = [
  {
    year: '2009',
    title: 'Started Consulting Journey',
    description: 'Began helping small businesses optimize their operations and marketing strategies.',
  },
  {
    year: '2012',
    title: 'Referral Marketing Focus',
    description: 'Developed specialized expertise in word-of-mouth and referral marketing systems.',
  },
  {
    year: '2015',
    title: 'Joint Venture Mastery',
    description: 'Expanded into strategic partnership development and joint venture facilitation.',
  },
  {
    year: '2018',
    title: 'Continuous Improvement Framework',
    description: 'Created a comprehensive methodology for sustainable business growth.',
  },
  {
    year: '2024',
    title: 'AI Integration',
    description: 'Incorporating AI tools and strategies to help clients stay ahead of the curve.',
  },
]

const values = [
  {
    icon: 'heroicons:light-bulb-20-solid',
    title: 'Continuous Improvement',
    description: 'Always seeking ways to enhance, optimize, and grow.',
  },
  {
    icon: 'heroicons:shield-check-20-solid',
    title: 'Integrity First',
    description: 'Building trust through honest, transparent relationships.',
  },
  {
    icon: 'heroicons:users-20-solid',
    title: 'Collaboration',
    description: 'Working together to achieve extraordinary results.',
  },
  {
    icon: 'heroicons:chart-bar-20-solid',
    title: 'Results Driven',
    description: 'Focused on measurable outcomes that matter.',
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

      <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid lg:grid-cols-2 gap-12 items-center">
          <div>
            <span class="inline-block px-4 py-1.5 bg-white/10 text-primary-300 text-sm font-semibold rounded-full mb-6">
              About Me
            </span>
            <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-display text-white mb-6">
              Hi, I'm
              <span class="bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
                Anatolii Petrenko
              </span>
            </h1>
            <p class="text-xl text-dark-300 leading-relaxed">
              AI Full-Stack Developer for Web & Mobile Apps
            </p>
          </div>

          <!-- Profile Card -->
          <div class="relative">
            <div class="bg-white/10 backdrop-blur-xl rounded-3xl border border-white/20 p-8 max-w-md mx-auto">
              <div class="w-32 h-32 rounded-2xl mx-auto mb-6 overflow-hidden shadow-xl">
                <img src="/compressed_image.jpg" alt="Anatolii Petrenko" class="w-full h-full object-cover" />
              </div>
              <h2 class="text-2xl font-bold text-white text-center mb-2">Anatolii Petrenko</h2>
              <p class="text-primary-300 text-center mb-6">Business Growth Strategist</p>
              <div class="grid grid-cols-3 gap-4 text-center">
                <div>
                  <div class="text-2xl font-bold text-white">15+</div>
                  <div class="text-sm text-dark-400">Years</div>
                </div>
                <div>
                  <div class="text-2xl font-bold text-white">500+</div>
                  <div class="text-sm text-dark-400">Clients</div>
                </div>
                <div>
                  <div class="text-2xl font-bold text-white">10x</div>
                  <div class="text-sm text-dark-400">Avg ROI</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Story -->
    <section class="py-24 bg-white">
      <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="prose prose-lg mx-auto text-dark-600">
          <h2 class="section-title text-center mb-12">
            My <span class="gradient-text">Story</span>
          </h2>

          <p class="text-xl leading-relaxed">
            Hello! I'm a Full-Stack AI Developer specialized in building scalable web and mobile applications that turn ideas into profitable digital products.
          </p>

          <p class="leading-relaxed">
            I combine strong engineering skills with modern AI technologies to help businesses automate processes, improve user experience, and launch powerful platforms faster.
          </p>

          <p class="leading-relaxed">
            I don't just write code. I design systems that are easy to manage, scalable to grow, and built for real users.
          </p>

          <h3>My Expertise</h3>

          <p class="leading-relaxed"><strong>1. Full-Stack Web Development</strong><br/>
            Building robust and scalable platforms using React, Next.js, Node.js, PHP, and Python.</p>

          <p class="leading-relaxed"><strong>2. Mobile App Development</strong><br/>
            Cross-platform iOS & Android apps using Flutter and React Native with user-focused UI/UX.</p>

          <p class="leading-relaxed"><strong>3. AI Systems & Automation</strong><br/>
            GPT-powered chatbots, AI agents for workflow automation, RAG-based knowledge systems, AI content generation platforms.</p>

          <p class="leading-relaxed"><strong>4. Automation & Integrations</strong><br/>
            n8n and Zapier workflow automation, WhatsApp & Instagram API integrations, Payment gateways, CRM, ERP system integrations.</p>

          <h3>What I Deliver</h3>

          <ul>
            <li>Clear understanding of business needs</li>
            <li>Clean, maintainable, and scalable architecture</li>
            <li>Fast and reliable delivery</li>
            <li>Solutions that reduce operational costs</li>
            <li>MVP development for startups and scalable systems for enterprises</li>
          </ul>

          <p class="leading-relaxed">If you are:</p>
          <ul>
            <li>Launching a startup and need a technical partner</li>
            <li>Looking to automate business processes with AI</li>
            <li>Building a SaaS platform</li>
            <li>Modernizing legacy systems</li>
            <li>Creating high-performance mobile apps</li>
          </ul>

          <p class="leading-relaxed">I can help you turn your vision into a reliable product.</p>

          <h3>Work Style</h3>

          <ul>
            <li>Clear and fast communication</li>
            <li>Respect for deadlines</li>
            <li>Problem-solving mindset</li>
            <li>Long-term partnership focus</li>
            <li>Security and performance-oriented development</li>
          </ul>

          <p class="leading-relaxed">
            My goal is to become a trusted technical partner who helps your business grow through smart technology.
          </p>
        </div>
      </div>
    </section>

    <!-- Values -->
    <section class="py-24 bg-dark-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            Values
          </span>
          <h2 class="section-title mb-4">
            What I <span class="gradient-text">Stand For</span>
          </h2>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="value in values"
            :key="value.title"
            class="text-center"
          >
            <div class="w-16 h-16 bg-primary-100 rounded-2xl flex items-center justify-center mx-auto mb-4">
              <Icon :name="value.icon" class="w-8 h-8 text-primary-600" />
            </div>
            <h3 class="text-xl font-bold text-dark-900 mb-2">{{ value.title }}</h3>
            <p class="text-dark-500">{{ value.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Timeline -->
    <section class="py-24 bg-white">
      <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            Journey
          </span>
          <h2 class="section-title mb-4">
            The <span class="gradient-text">Path</span> So Far
          </h2>
        </div>

        <div class="relative">
          <!-- Timeline Line -->
          <div class="absolute left-8 md:left-1/2 top-0 bottom-0 w-0.5 bg-dark-200 transform md:-translate-x-1/2"></div>

          <div class="space-y-12">
            <div
              v-for="(item, index) in timeline"
              :key="item.year"
              class="relative flex items-start md:items-center"
              :class="index % 2 === 0 ? 'md:flex-row' : 'md:flex-row-reverse'"
            >
              <!-- Dot -->
              <div class="absolute left-8 md:left-1/2 w-4 h-4 bg-primary-600 rounded-full transform -translate-x-1/2 z-10"></div>

              <!-- Content -->
              <div class="ml-20 md:ml-0 md:w-1/2 md:px-12">
                <div
                  class="bg-white rounded-xl p-6 shadow-lg border border-dark-100"
                  :class="index % 2 === 0 ? 'md:text-right' : 'md:text-left'"
                >
                  <span class="text-primary-600 font-bold text-lg">{{ item.year }}</span>
                  <h3 class="text-xl font-bold text-dark-900 mt-1 mb-2">{{ item.title }}</h3>
                  <p class="text-dark-500">{{ item.description }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <SectionsCTASection />
  </div>
</template>
