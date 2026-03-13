<script setup lang="ts">
useSeoMeta({
  title: 'Blog | Anatolii Petrenko',
  description: 'Insights and strategies for business growth, referral marketing, joint ventures, and continuous improvement.',
})

const posts = [
  {
    slug: 'need-more-sales',
    title: 'I Need More Sales: A Strategic Approach to Growth',
    excerpt: 'Discover proven strategies to increase your sales without burning out your team or sacrificing customer relationships. Learn how to build sustainable revenue systems.',
    category: 'Sales Strategy',
    date: '2024-12-15',
    readTime: '5 min read',
    featured: true,
  },
  {
    slug: 'referral-software-grow-business',
    title: 'Can Referral Software Help Me Grow My Business?',
    excerpt: 'Explore how modern referral marketing tools can automate and scale your word-of-mouth marketing efforts for consistent lead generation.',
    category: 'Referral Marketing',
    date: '2024-12-10',
    readTime: '7 min read',
    featured: false,
  },
  {
    slug: 'time-focus-mini-day-challenge',
    title: 'Life Optimizers: Time Focus and the Mini Day Challenge',
    excerpt: 'Learn the mini day challenge technique to maximize productivity and achieve more in less time without sacrificing quality or wellbeing.',
    category: 'Productivity',
    date: '2024-12-05',
    readTime: '4 min read',
    featured: false,
  },
  {
    slug: 'velore-networks-blockchain-marketing',
    title: 'Velore Networks: The Future of Relationship Marketing',
    excerpt: 'An introduction to blockchain-powered relationship marketing and how it\'s changing the way businesses connect with customers.',
    category: 'Innovation',
    date: '2024-11-28',
    readTime: '6 min read',
    featured: false,
  },
  {
    slug: 'empiring-business-framework',
    title: 'Empiring: A New Framework for Business Growth',
    excerpt: 'Introducing the Empiring framework - a comprehensive approach to building and scaling mission-driven businesses.',
    category: 'Strategy',
    date: '2024-11-20',
    readTime: '8 min read',
    featured: false,
  },
  {
    slug: 'joint-venture-success-secrets',
    title: 'The Secret to Successful Joint Ventures',
    excerpt: 'Learn the key principles that make joint ventures succeed and how to avoid the common pitfalls that derail partnerships.',
    category: 'Joint Ventures',
    date: '2024-11-15',
    readTime: '6 min read',
    featured: false,
  },
]

const categories = ['All', 'Sales Strategy', 'Referral Marketing', 'Productivity', 'Innovation', 'Strategy', 'Joint Ventures']

const selectedCategory = ref('All')

const filteredPosts = computed(() => {
  if (selectedCategory.value === 'All') return posts
  return posts.filter(post => post.category === selectedCategory.value)
})

const featuredPost = computed(() => posts.find(p => p.featured))

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
    <section class="pt-32 pb-20 bg-gradient-to-br from-dark-900 via-dark-800 to-primary-900 relative overflow-hidden">
      <div class="absolute inset-0">
        <div class="absolute top-1/4 -left-20 w-96 h-96 bg-primary-500/20 rounded-full blur-3xl"></div>
        <div class="absolute bottom-1/4 -right-20 w-80 h-80 bg-secondary-500/20 rounded-full blur-3xl"></div>
      </div>

      <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <span class="inline-block px-4 py-1.5 bg-white/10 text-primary-300 text-sm font-semibold rounded-full mb-6">
          Blog
        </span>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-display text-white mb-6">
          Insights &
          <span class="bg-gradient-to-r from-primary-400 to-secondary-400 bg-clip-text text-transparent">
            Strategies
          </span>
        </h1>
        <p class="text-xl text-dark-300 max-w-2xl mx-auto">
          Actionable strategies and insights to help you grow your business, build partnerships, and achieve sustainable success.
        </p>
      </div>
    </section>

    <!-- Featured Post -->
    <section v-if="featuredPost" class="py-16 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="bg-gradient-to-br from-primary-50 to-secondary-50 rounded-3xl overflow-hidden">
          <div class="grid lg:grid-cols-2 gap-8 p-8 lg:p-12">
            <!-- Image -->
            <div class="aspect-video lg:aspect-auto bg-gradient-to-br from-primary-100 to-secondary-100 rounded-2xl flex items-center justify-center">
              <Icon name="heroicons:document-text-20-solid" class="w-24 h-24 text-primary-300" />
            </div>

            <!-- Content -->
            <div class="flex flex-col justify-center">
              <div class="flex items-center space-x-3 mb-4">
                <span class="px-3 py-1 bg-primary-600 text-white text-xs font-semibold rounded-full">
                  Featured
                </span>
                <span
                  class="px-3 py-1 text-xs font-semibold rounded-full"
                  :class="categoryColors[featuredPost.category]"
                >
                  {{ featuredPost.category }}
                </span>
              </div>
              <h2 class="text-2xl lg:text-3xl font-bold text-dark-900 mb-4">
                <NuxtLink :to="`/blog/${featuredPost.slug}`" class="hover:text-primary-600 transition-colors">
                  {{ featuredPost.title }}
                </NuxtLink>
              </h2>
              <p class="text-dark-500 mb-6 leading-relaxed">
                {{ featuredPost.excerpt }}
              </p>
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-4 text-sm text-dark-400">
                  <span>{{ formatDate(featuredPost.date) }}</span>
                  <span>&bull;</span>
                  <span>{{ featuredPost.readTime }}</span>
                </div>
                <NuxtLink
                  :to="`/blog/${featuredPost.slug}`"
                  class="text-primary-600 font-semibold flex items-center hover:text-primary-700 transition-colors"
                >
                  Read Article
                  <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-1" />
                </NuxtLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- All Posts -->
    <section class="py-16 bg-dark-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <!-- Category Filter -->
        <div class="flex flex-wrap gap-2 mb-12">
          <button
            v-for="category in categories"
            :key="category"
            class="px-4 py-2 rounded-full text-sm font-medium transition-all"
            :class="selectedCategory === category
              ? 'bg-primary-600 text-white'
              : 'bg-white text-dark-600 hover:bg-dark-100'"
            @click="selectedCategory = category"
          >
            {{ category }}
          </button>
        </div>

        <!-- Posts Grid -->
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <article
            v-for="post in filteredPosts"
            :key="post.slug"
            class="group card overflow-hidden"
          >
            <!-- Image -->
            <div class="aspect-video bg-gradient-to-br from-primary-100 to-secondary-100 relative overflow-hidden">
              <div class="absolute inset-0 flex items-center justify-center">
                <Icon name="heroicons:document-text-20-solid" class="w-16 h-16 text-primary-300" />
              </div>
              <div class="absolute inset-0 bg-dark-900/0 group-hover:bg-dark-900/10 transition-colors duration-300"></div>
            </div>

            <!-- Content -->
            <div class="p-6">
              <div class="flex items-center space-x-3 mb-4">
                <span
                  class="px-3 py-1 text-xs font-semibold rounded-full"
                  :class="categoryColors[post.category] || 'bg-dark-100 text-dark-600'"
                >
                  {{ post.category }}
                </span>
                <span class="text-sm text-dark-400">{{ post.readTime }}</span>
              </div>

              <h3 class="text-lg font-bold text-dark-900 mb-2 group-hover:text-primary-600 transition-colors line-clamp-2">
                <NuxtLink :to="`/blog/${post.slug}`">
                  {{ post.title }}
                </NuxtLink>
              </h3>

              <p class="text-dark-500 text-sm mb-4 line-clamp-3">
                {{ post.excerpt }}
              </p>

              <div class="flex items-center justify-between pt-4 border-t border-dark-100">
                <span class="text-sm text-dark-400">{{ formatDate(post.date) }}</span>
                <NuxtLink
                  :to="`/blog/${post.slug}`"
                  class="text-primary-600 font-semibold text-sm flex items-center hover:text-primary-700 transition-colors"
                >
                  Read More
                  <Icon name="heroicons:arrow-right-20-solid" class="w-4 h-4 ml-1" />
                </NuxtLink>
              </div>
            </div>
          </article>
        </div>

        <!-- Empty State -->
        <div v-if="filteredPosts.length === 0" class="text-center py-16">
          <Icon name="heroicons:document-magnifying-glass-20-solid" class="w-16 h-16 text-dark-300 mx-auto mb-4" />
          <h3 class="text-xl font-bold text-dark-900 mb-2">No posts found</h3>
          <p class="text-dark-500">Try selecting a different category.</p>
        </div>
      </div>
    </section>

    <!-- Newsletter CTA -->
    <section class="py-24 bg-white">
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <Icon name="heroicons:envelope-20-solid" class="w-16 h-16 text-primary-600 mx-auto mb-6" />
        <h2 class="section-title mb-4">
          Subscribe to the <span class="gradient-text">Newsletter</span>
        </h2>
        <p class="text-lg text-dark-500 mb-8">
          Get weekly insights on business growth, marketing strategies, and continuous improvement delivered to your inbox.
        </p>
        <form class="flex flex-col sm:flex-row gap-4 max-w-md mx-auto">
          <input
            type="email"
            placeholder="Enter your email"
            class="flex-1 px-4 py-3 bg-dark-50 border border-dark-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all outline-none"
          />
          <button type="submit" class="btn-primary">
            Subscribe
          </button>
        </form>
        <p class="text-sm text-dark-400 mt-4">No spam, unsubscribe anytime.</p>
      </div>
    </section>
  </div>
</template>
