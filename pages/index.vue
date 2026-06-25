<script setup lang="ts">
// The homepage is the book — a full, scroll-driven experience with no global
// header/footer chrome. Other routes keep the standard layout.
definePageMeta({ layout: false })

useSeoMeta({
  title: 'Kato Himari | AI Full-Stack Developer',
  description: 'The portfolio of Kato Himari, AI Full-Stack Developer — presented as an interactive book. Scroll to open the cover and turn through each chapter.',
})
</script>

<template>
  <BookExperience />
</template>
