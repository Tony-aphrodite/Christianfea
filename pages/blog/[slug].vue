<script setup lang="ts">
const route = useRoute()

// In a real app, this would fetch from an API or CMS
const posts: Record<string, any> = {
  'need-more-sales': {
    title: 'I Need More Sales: A Strategic Approach to Growth',
    excerpt: 'Discover proven strategies to increase your sales without burning out your team or sacrificing customer relationships.',
    category: 'Sales Strategy',
    date: '2024-12-15',
    readTime: '5 min read',
    content: `
      <p class="lead">Every entrepreneur has uttered these words at some point: "I need more sales." It's the lifeblood of business, yet for many, it remains an elusive goal that seems to require more effort, more time, and more resources than they have available.</p>

      <h2>The Problem with Traditional Sales Approaches</h2>
      <p>Most businesses approach sales with a "more is better" mentality. More cold calls, more emails, more advertising spend. But this approach often leads to diminishing returns and burnout.</p>

      <p>The truth is, sustainable sales growth doesn't come from working harder—it comes from working smarter. It requires a strategic approach that focuses on:</p>

      <ul>
        <li><strong>Building relationships</strong> rather than chasing transactions</li>
        <li><strong>Creating value</strong> before asking for the sale</li>
        <li><strong>Leveraging referrals</strong> from satisfied customers</li>
        <li><strong>Developing partnerships</strong> that expand your reach</li>
      </ul>

      <h2>The Referral Advantage</h2>
      <p>Referral marketing is one of the most underutilized yet powerful sales strategies available. When a satisfied customer refers you to someone in their network, you're not starting from zero—you're starting with trust already established.</p>

      <p>Studies consistently show that referred customers:</p>
      <ul>
        <li>Have higher conversion rates</li>
        <li>Spend more on average</li>
        <li>Have longer customer lifetime values</li>
        <li>Are more likely to refer others themselves</li>
      </ul>

      <h2>Building Your Referral Engine</h2>
      <p>The key to sustainable sales growth is building a systematic referral engine. This isn't about occasionally asking customers for referrals—it's about creating a repeatable process that generates leads consistently.</p>

      <h3>Step 1: Deliver Exceptional Value</h3>
      <p>Before you can ask for referrals, you need to give customers something worth talking about. Focus on exceeding expectations at every touchpoint.</p>

      <h3>Step 2: Make Referrals Easy</h3>
      <p>Don't make customers work to refer you. Provide them with simple tools and clear instructions for sharing your business with their network.</p>

      <h3>Step 3: Show Appreciation</h3>
      <p>Recognize and reward customers who refer others. This doesn't always mean monetary incentives—sometimes a simple thank you and recognition goes further.</p>

      <h2>Taking Action</h2>
      <p>If you're ready to build a sustainable sales engine for your business, start by auditing your current approach. Ask yourself:</p>

      <ul>
        <li>How many of my new customers come from referrals?</li>
        <li>Do I have a systematic process for generating referrals?</li>
        <li>Am I creating experiences worth talking about?</li>
      </ul>

      <p>The answers to these questions will reveal opportunities for growth that don't require working harder—just working smarter.</p>
    `,
  },
  'referral-software-grow-business': {
    title: 'Can Referral Software Help Me Grow My Business?',
    excerpt: 'Explore how modern referral marketing tools can automate and scale your word-of-mouth marketing efforts.',
    category: 'Referral Marketing',
    date: '2024-12-10',
    readTime: '7 min read',
    content: `
      <p class="lead">In the digital age, word-of-mouth marketing has evolved beyond casual recommendations. Referral software has emerged as a powerful tool for businesses looking to systematize and scale their referral programs.</p>

      <h2>What Is Referral Software?</h2>
      <p>Referral software is a category of tools designed to automate the process of acquiring new customers through existing customer recommendations. These platforms typically provide features like:</p>

      <ul>
        <li>Unique referral links for each customer</li>
        <li>Automated reward tracking and distribution</li>
        <li>Analytics and performance monitoring</li>
        <li>Integration with your existing CRM and marketing tools</li>
      </ul>

      <h2>The Benefits of Using Referral Software</h2>

      <h3>Automation at Scale</h3>
      <p>Manual referral tracking quickly becomes unmanageable as your customer base grows. Software automates the tedious parts—tracking who referred whom, calculating rewards, and sending notifications.</p>

      <h3>Data-Driven Optimization</h3>
      <p>Modern referral platforms provide analytics that help you understand which customers are your best advocates, which incentives work best, and where your program might be falling short.</p>

      <h3>Consistent Customer Experience</h3>
      <p>Automation ensures every customer has the same referral experience, from the invitation they receive to the reward they earn.</p>

      <h2>Is Referral Software Right for You?</h2>
      <p>Before investing in referral software, consider these factors:</p>

      <ul>
        <li><strong>Customer base size:</strong> If you have fewer than 100 customers, a simple manual process might suffice</li>
        <li><strong>Product/market fit:</strong> Do customers naturally talk about your product?</li>
        <li><strong>Resources:</strong> Can you commit to managing and optimizing the program?</li>
      </ul>

      <p>The best referral software in the world won't help if your underlying product or service doesn't inspire advocacy. Focus on delivering value first, then leverage technology to amplify word-of-mouth.</p>
    `,
  },
  'time-focus-mini-day-challenge': {
    title: 'Life Optimizers: Time Focus and the Mini Day Challenge',
    excerpt: 'Learn the mini day challenge technique to maximize productivity and achieve more in less time.',
    category: 'Productivity',
    date: '2024-12-05',
    readTime: '4 min read',
    content: `
      <p class="lead">Time is our most precious resource. Unlike money, we can't earn more of it. The mini day challenge is a productivity technique designed to help you make the most of every working hour.</p>

      <h2>The Mini Day Concept</h2>
      <p>Instead of viewing your workday as one continuous block, the mini day challenge divides it into smaller, focused periods—typically 90 minutes each. Each mini day has:</p>

      <ul>
        <li>A clear objective</li>
        <li>A defined start and end time</li>
        <li>Minimal distractions</li>
        <li>A brief review period</li>
      </ul>

      <h2>Why It Works</h2>
      <p>The science behind the mini day approach aligns with our natural energy cycles. Research shows that our ability to focus intensely follows 90-minute cycles throughout the day.</p>

      <p>By working with these natural rhythms rather than against them, you can achieve more with less effort and end each day feeling accomplished rather than drained.</p>

      <h2>Implementing the Mini Day Challenge</h2>

      <h3>Step 1: Audit Your Current Day</h3>
      <p>Track how you currently spend your time. Most people discover they have fewer productive hours than they think.</p>

      <h3>Step 2: Design Your Mini Days</h3>
      <p>Plan 3-4 mini days within your workday, each focused on a specific type of task or project.</p>

      <h3>Step 3: Protect Your Boundaries</h3>
      <p>The challenge is maintaining focus during each mini day. Turn off notifications, close unnecessary tabs, and communicate your availability to colleagues.</p>

      <h2>The Results</h2>
      <p>Entrepreneurs who implement the mini day challenge consistently report completing more meaningful work while feeling less stressed. The key is consistency—give it two weeks before evaluating results.</p>
    `,
  },
}

const post = computed(() => posts[route.params.slug as string])

if (!post.value) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Post Not Found',
  })
}

useSeoMeta({
  title: `${post.value.title} | Anatolii Petrenko`,
  description: post.value.excerpt,
})

const categoryColors: Record<string, string> = {
  'Sales Strategy': 'bg-blue-100 text-blue-700',
  'Referral Marketing': 'bg-green-100 text-green-700',
  'Productivity': 'bg-purple-100 text-purple-700',
  'Innovation': 'bg-orange-100 text-orange-700',
  'Strategy': 'bg-pink-100 text-pink-700',
  'Joint Ventures': 'bg-cyan-100 text-cyan-700',
}

function formatDate(dateString: string) {
  return new Date(dateString).toLocaleDateString('en-US', {
    month: 'long',
    day: 'numeric',
    year: 'numeric',
  })
}
</script>

<template>
  <div>
    <!-- Hero -->
    <section class="pt-32 pb-16 bg-gradient-to-br from-dark-900 via-dark-800 to-primary-900 relative overflow-hidden">
      <div class="absolute inset-0">
        <div class="absolute top-1/4 -left-20 w-96 h-96 bg-primary-500/20 rounded-full blur-3xl"></div>
        <div class="absolute bottom-1/4 -right-20 w-80 h-80 bg-secondary-500/20 rounded-full blur-3xl"></div>
      </div>

      <div class="relative max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
        <NuxtLink to="/blog" class="inline-flex items-center text-primary-300 hover:text-primary-200 mb-6 transition-colors">
          <Icon name="heroicons:arrow-left-20-solid" class="w-5 h-5 mr-2" />
          Back to Blog
        </NuxtLink>

        <div class="flex items-center space-x-3 mb-6">
          <span
            class="px-3 py-1 text-sm font-semibold rounded-full"
            :class="categoryColors[post.category] || 'bg-dark-100 text-dark-600'"
          >
            {{ post.category }}
          </span>
          <span class="text-dark-400">{{ post.readTime }}</span>
        </div>

        <h1 class="text-3xl sm:text-4xl lg:text-5xl font-bold font-display text-white mb-6 leading-tight">
          {{ post.title }}
        </h1>

        <div class="flex items-center space-x-4">
          <div class="w-12 h-12 rounded-full overflow-hidden">
            <img src="/compressed_image.jpg" alt="Anatolii Petrenko" class="w-full h-full object-cover" />
          </div>
          <div>
            <div class="text-white font-medium">Anatolii Petrenko</div>
            <div class="text-dark-400 text-sm">{{ formatDate(post.date) }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Content -->
    <article class="py-16 bg-white">
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
        <div
          class="prose prose-lg max-w-none
            prose-headings:font-display prose-headings:text-dark-900
            prose-p:text-dark-600 prose-p:leading-relaxed
            prose-a:text-primary-600 prose-a:no-underline hover:prose-a:underline
            prose-strong:text-dark-800
            prose-ul:text-dark-600 prose-ol:text-dark-600
            prose-li:marker:text-primary-500"
          v-html="post.content"
        ></div>

        <!-- Share -->
        <div class="mt-12 pt-8 border-t border-dark-200">
          <div class="flex items-center justify-between flex-wrap gap-4">
            <div>
              <span class="text-dark-500 text-sm">Share this article:</span>
              <div class="flex space-x-2 mt-2">
                <a href="#" class="w-10 h-10 bg-dark-100 rounded-lg flex items-center justify-center text-dark-500 hover:bg-primary-100 hover:text-primary-600 transition-colors">
                  <Icon name="mdi:twitter" class="w-5 h-5" />
                </a>
                <a href="#" class="w-10 h-10 bg-dark-100 rounded-lg flex items-center justify-center text-dark-500 hover:bg-primary-100 hover:text-primary-600 transition-colors">
                  <Icon name="mdi:linkedin" class="w-5 h-5" />
                </a>
                <a href="#" class="w-10 h-10 bg-dark-100 rounded-lg flex items-center justify-center text-dark-500 hover:bg-primary-100 hover:text-primary-600 transition-colors">
                  <Icon name="mdi:facebook" class="w-5 h-5" />
                </a>
              </div>
            </div>

            <NuxtLink to="/contact" class="btn-primary">
              Work With Me
              <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
            </NuxtLink>
          </div>
        </div>
      </div>
    </article>

    <!-- Author Bio -->
    <section class="py-16 bg-dark-50">
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="bg-white rounded-2xl p-8 shadow-xl">
          <div class="flex flex-col sm:flex-row items-center sm:items-start gap-6">
            <div class="w-24 h-24 rounded-2xl overflow-hidden flex-shrink-0">
              <img src="/compressed_image.jpg" alt="Anatolii Petrenko" class="w-full h-full object-cover" />
            </div>
            <div>
              <h3 class="text-xl font-bold text-dark-900 mb-2">About Anatolii Petrenko</h3>
              <p class="text-dark-500 mb-4">
                Anatolii Petrenko is a business growth strategist who helps mission-based entrepreneurs achieve sustainable growth through referral marketing, joint ventures, and continuous improvement methodologies.
              </p>
              <NuxtLink to="/about" class="text-primary-600 font-semibold hover:text-primary-700 inline-flex items-center">
                Learn more about Anatolii
                <Icon name="heroicons:arrow-right-20-solid" class="w-4 h-4 ml-1" />
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <SectionsCTASection />
  </div>
</template>
