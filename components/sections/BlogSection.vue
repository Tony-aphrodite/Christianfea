<script setup lang="ts">
const posts = [
  {
    slug: 'need-more-sales',
    title: 'I Need More Sales: A Strategic Approach to Growth',
    excerpt: 'Discover proven strategies to increase your sales without burning out your team or sacrificing customer relationships.',
    category: 'Sales Strategy',
    date: '2024-12-15',
    readTime: '5 min read',
    image: null,
  },
  {
    slug: 'referral-software-grow-business',
    title: 'Can Referral Software Help Me Grow My Business?',
    excerpt: 'Explore how modern referral marketing tools can automate and scale your word-of-mouth marketing efforts.',
    category: 'Referral Marketing',
    date: '2024-12-10',
    readTime: '7 min read',
    image: null,
  },
  {
    slug: 'time-focus-mini-day-challenge',
    title: 'Life Optimizers: Time Focus and the Mini Day Challenge',
    excerpt: 'Learn the mini day challenge technique to maximize productivity and achieve more in less time.',
    category: 'Productivity',
    date: '2024-12-05',
    readTime: '4 min read',
    image: null,
  },
]

const categoryColors: Record<string, string> = {
  'Sales Strategy': 'bg-blue-100 text-blue-700',
  'Referral Marketing': 'bg-green-100 text-green-700',
  'Productivity': 'bg-purple-100 text-purple-700',
}

function formatDate(dateString: string) {
  return new Date(dateString).toLocaleDateString('en-US', {
    month: 'short',
    day: 'numeric',
    year: 'numeric',
  })
}
</script>

<template>
  <section id="blog" class="py-24 bg-dark-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="flex flex-col md:flex-row md:items-end md:justify-between mb-12">
        <div>
          <span class="inline-block px-4 py-1.5 bg-primary-100 text-primary-700 text-sm font-semibold rounded-full mb-4">
            Blog
          </span>
          <h2 class="section-title mb-4">
            Latest
            <span class="gradient-text">Insights</span>
          </h2>
          <p class="section-subtitle">
            Actionable strategies and insights to help you grow your business.
          </p>
        </div>
        <NuxtLink to="/blog" class="btn-secondary mt-6 md:mt-0">
          View All Posts
          <Icon name="heroicons:arrow-right-20-solid" class="w-5 h-5 ml-2" />
        </NuxtLink>
      </div>

      <!-- Blog Grid -->
      <div class="grid md:grid-cols-3 gap-8">
        <article
          v-for="post in posts"
          :key="post.slug"
          class="group card overflow-hidden"
        >
          <!-- Image Placeholder -->
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

            <p class="text-dark-500 text-sm mb-4 line-clamp-2">
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
    </div>
  </section>
</template>
