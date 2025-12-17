<script setup lang="ts">
useSeoMeta({
  title: 'Services | Christian Fea',
  description: 'Explore comprehensive business consulting services including growth strategy, referral marketing, joint ventures, and business optimization.',
})

const services = [
  {
    id: 'consulting',
    icon: 'heroicons:rocket-launch-20-solid',
    title: 'Business Growth Strategy',
    description: 'Develop a comprehensive roadmap for sustainable growth with actionable strategies tailored to your unique business goals and market position.',
    benefits: [
      'Custom growth roadmap development',
      'Market opportunity analysis',
      'Competitive positioning strategy',
      'Revenue diversification planning',
      'Scalability assessment and planning',
      'Performance metrics and KPI development',
    ],
    color: 'primary',
  },
  {
    id: 'referral',
    icon: 'heroicons:user-group-20-solid',
    title: 'Referral Marketing',
    description: 'Harness the power of word-of-mouth marketing to generate high-quality leads and build lasting customer relationships that fuel organic growth.',
    benefits: [
      'Referral program design and implementation',
      'Customer advocacy strategy',
      'Incentive structure optimization',
      'Referral tracking systems',
      'Word-of-mouth amplification',
      'Customer loyalty programs',
    ],
    color: 'secondary',
  },
  {
    id: 'ventures',
    icon: 'heroicons:puzzle-piece-20-solid',
    title: 'Joint Ventures & Strategic Alliances',
    description: 'Create strategic partnerships and alliances that multiply your reach and accelerate business growth through collaborative opportunities.',
    benefits: [
      'Partner identification and vetting',
      'Deal structure and negotiation',
      'Collaboration strategy development',
      'Risk assessment and mitigation',
      'Joint marketing initiatives',
      'Revenue sharing models',
    ],
    color: 'primary',
  },
  {
    id: 'optimization',
    icon: 'heroicons:cog-8-tooth-20-solid',
    title: 'Business Optimization',
    description: 'Streamline operations, eliminate inefficiencies, and maximize profitability through continuous improvement methodologies and data-driven decisions.',
    benefits: [
      'Process audit and improvement',
      'Operational efficiency analysis',
      'Cost reduction strategies',
      'Workflow automation',
      'Team productivity enhancement',
      'Performance management systems',
    ],
    color: 'secondary',
  },
]

const process = [
  {
    step: 1,
    title: 'Discovery Call',
    description: 'We start with a free consultation to understand your business, challenges, and goals.',
  },
  {
    step: 2,
    title: 'Strategic Analysis',
    description: 'I conduct a thorough analysis of your current situation and identify opportunities for growth.',
  },
  {
    step: 3,
    title: 'Custom Strategy',
    description: 'Together, we develop a tailored action plan with clear milestones and measurable outcomes.',
  },
  {
    step: 4,
    title: 'Implementation',
    description: 'I provide hands-on support as you implement the strategy, adjusting as needed.',
  },
  {
    step: 5,
    title: 'Optimization',
    description: 'We continuously monitor results and optimize for maximum impact and ROI.',
  },
]

const colorClasses = {
  primary: {
    bg: 'bg-primary-100',
    icon: 'text-primary-600',
    border: 'border-primary-200',
  },
  secondary: {
    bg: 'bg-secondary-100',
    icon: 'text-secondary-600',
    border: 'border-secondary-200',
  },
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
          Services
        </span>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-display text-white mb-6">
          Comprehensive Solutions for
          <span class="block mt-2 bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Business Growth
          </span>
        </h1>
        <p class="text-xl text-dark-300 max-w-2xl mx-auto">
          From strategy development to implementation, I provide the expertise and support you need to achieve sustainable, long-term success.
        </p>
      </div>
    </section>

    <!-- Services Detail -->
    <section class="py-24 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="space-y-24">
          <div
            v-for="(service, index) in services"
            :key="service.id"
            :id="service.id"
            class="scroll-mt-24"
          >
            <div
              class="grid lg:grid-cols-2 gap-12 items-center"
              :class="index % 2 === 1 ? 'lg:flex-row-reverse' : ''"
            >
              <!-- Content -->
              <div :class="index % 2 === 1 ? 'lg:order-2' : ''">
                <div
                  class="w-16 h-16 rounded-2xl flex items-center justify-center mb-6"
                  :class="colorClasses[service.color].bg"
                >
                  <Icon
                    :name="service.icon"
                    class="w-8 h-8"
                    :class="colorClasses[service.color].icon"
                  />
                </div>
                <h2 class="text-3xl font-bold text-dark-900 mb-4">
                  {{ service.title }}
                </h2>
                <p class="text-lg text-dark-500 mb-8 leading-relaxed">
                  {{ service.description }}
                </p>

                <!-- Benefits -->
                <div class="grid sm:grid-cols-2 gap-4">
                  <div
                    v-for="benefit in service.benefits"
                    :key="benefit"
                    class="flex items-start space-x-3"
                  >
                    <Icon
                      name="heroicons:check-circle-20-solid"
                      class="w-5 h-5 text-green-500 flex-shrink-0 mt-0.5"
                    />
                    <span class="text-dark-600">{{ benefit }}</span>
                  </div>
                </div>
              </div>

              <!-- Visual -->
              <div :class="index % 2 === 1 ? 'lg:order-1' : ''">
                <div
                  class="aspect-square rounded-3xl flex items-center justify-center"
                  :class="colorClasses[service.color].bg"
                >
                  <Icon
                    :name="service.icon"
                    class="w-32 h-32"
                    :class="colorClasses[service.color].icon"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Process -->
    <section class="py-24 bg-dark-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            Process
          </span>
          <h2 class="section-title mb-4">
            How We
            <span class="gradient-text">Work Together</span>
          </h2>
          <p class="section-subtitle mx-auto">
            A proven process designed to deliver results efficiently and effectively.
          </p>
        </div>

        <div class="relative">
          <!-- Timeline Line -->
          <div class="hidden md:block absolute top-8 left-0 right-0 h-0.5 bg-dark-200"></div>

          <div class="grid md:grid-cols-5 gap-8">
            <div
              v-for="item in process"
              :key="item.step"
              class="relative"
            >
              <!-- Step Number -->
              <div class="w-16 h-16 bg-primary-600 text-white rounded-full flex items-center justify-center text-xl font-bold mx-auto mb-4 relative z-10">
                {{ item.step }}
              </div>
              <div class="text-center">
                <h3 class="font-bold text-dark-900 mb-2">{{ item.title }}</h3>
                <p class="text-sm text-dark-500">{{ item.description }}</p>
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
