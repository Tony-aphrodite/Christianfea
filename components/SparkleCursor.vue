<script setup lang="ts">
/*
 * Trails small white star-sparkles at the cursor as the mouse moves.
 * Sparkles are lightweight DOM spans that animate once and self-remove.
 * Disabled when the user prefers reduced motion; no effect on touch devices.
 */
const layer = ref<HTMLElement | null>(null)
let lastX = 0
let lastY = 0
let lastT = 0

function spawn(x: number, y: number, scale = 1) {
  const el = document.createElement('span')
  el.className = 'sparkle'
  const size = (6 + Math.random() * 8) * scale
  const jx = (Math.random() - 0.5) * 16
  const jy = (Math.random() - 0.5) * 16
  el.style.left = x + jx + 'px'
  el.style.top = y + jy + 'px'
  el.style.width = el.style.height = size + 'px'
  el.style.setProperty('--rot', Math.random() * 90 + 'deg')
  el.style.animationDuration = 600 + Math.random() * 450 + 'ms'
  el.addEventListener('animationend', () => el.remove())
  layer.value?.appendChild(el)
}

function onMove(e: MouseEvent) {
  const now = performance.now()
  const dist = Math.hypot(e.clientX - lastX, e.clientY - lastY)
  // throttle by time + distance so sparkles appear only "a little" at a time
  if (now - lastT < 28 || dist < 6) return
  lastT = now
  lastX = e.clientX
  lastY = e.clientY
  spawn(e.clientX, e.clientY)
  if (Math.random() < 0.35) spawn(e.clientX, e.clientY, 0.6) // occasional tiny twin
}

onMounted(() => {
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return
  window.addEventListener('mousemove', onMove, { passive: true })
})
onUnmounted(() => window.removeEventListener('mousemove', onMove))
</script>

<template>
  <div ref="layer" class="sparkle-layer" aria-hidden="true"></div>
</template>

<!-- not scoped: sparkle spans are created at runtime, outside the SFC template -->
<style>
.sparkle-layer {
  position: fixed;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
  z-index: 99999;
}
.sparkle {
  position: fixed;
  background: #ffffff;
  clip-path: polygon(50% 0%, 60% 40%, 100% 50%, 60% 60%, 50% 100%, 40% 60%, 0% 50%, 40% 40%);
  filter: drop-shadow(0 0 4px rgba(255, 255, 255, 0.9));
  transform: translate(-50%, -50%) scale(0) rotate(var(--rot, 0deg));
  animation-name: sparkle-pop;
  animation-timing-function: ease-out;
  animation-fill-mode: forwards;
  will-change: transform, opacity;
}
@keyframes sparkle-pop {
  0% { transform: translate(-50%, -50%) scale(0) rotate(var(--rot, 0deg)); opacity: 0; }
  35% { transform: translate(-50%, -50%) scale(1) rotate(calc(var(--rot, 0deg) + 18deg)); opacity: 1; }
  100% { transform: translate(-50%, -50%) scale(0.15) rotate(calc(var(--rot, 0deg) + 55deg)); opacity: 0; }
}
</style>
