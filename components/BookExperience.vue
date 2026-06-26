<script setup lang="ts">
/*
 * Scroll-driven 3D book. The whole portfolio is one book: scrolling opens the
 * cover and turns each leaf, one section/spread at a time. Page content is
 * data-driven (see `faces` below) and rendered by <BookFace>; this file owns
 * the 3D mechanics, sizing and chrome.
 */
const clamp = (v: number, a: number, b: number) => Math.min(b, Math.max(a, v))
const PAGE_W = 440
const PAGE_H = 600
const FLIP = 0.62 // fraction of each scroll-unit spent flipping (rest = dwell)

// ---- portfolio data ----------------------------------------------------
const projects = [
  { file: 'Axelar.JPG', title: 'Axelar', category: 'Cross-Chain', description: 'A cross-chain interoperability network letting institutions like Citi, Deutsche Bank and Mastercard navigate a secure multichain world.', tech: ['React', 'Next.js', 'Solidity', 'Go'], url: '' },
  { file: 'ternoa.jpg', title: 'Ternoa', category: 'Web3 / Crypto', description: 'Landing site for an evolutionary NFT blockchain bringing web3 ideas to life — private content, delegation, renting, validators and staking.', tech: ['React', 'Next.js', 'Rust', 'Polkadot.js'], url: '' },
  { file: 'tofunft.jpg', title: 'tofuNFT', category: 'NFT Marketplace', description: 'A multi-chain NFT marketplace on BNB Chain with collection banners, a mint launchpad and trending hot collections with live sales activity.', tech: ['React', 'Next.js', 'Solidity', 'ethers.js'], url: 'tofunft.com' },
  { file: 'Creaticles.JPG', title: 'Creaticles', category: 'NFT Marketplace', description: 'A Web3 platform for NFT contests where users post requests and submit artwork, with USDT, ETH and FTM prize pools and wallet connection.', tech: ['React', 'Next.js', 'Solidity', 'IPFS'], url: '' },
  { file: 'iZUMi.png', title: 'iZUMi Finance', category: 'DeFi', description: 'A multi-chain DeFi protocol delivering programmable liquidity-as-a-service and concentrated liquidity market-making for on-chain liquidity.', tech: ['React', 'Next.js', 'Solidity', 'TypeScript'], url: '' },
  { file: 'Localcryptos.JPG', title: 'LocalCoinSwap', category: 'Web3 / Crypto', description: 'A non-custodial peer-to-peer crypto exchange supporting buy, sell, swap and cash trading with private-key access and free taker fees.', tech: ['Vue', 'Django', 'Python', 'Web3.js'], url: '' },
  { file: 'reefscan.jpg', title: 'ReefScan', category: 'Web3 / Crypto', description: 'A Reef blockchain explorer for searching blocks, accounts, transfers and contracts, with live network stats and latest finalized blocks.', tech: ['React', 'GraphQL', 'Polkadot.js', 'TypeScript'], url: '' },
  { file: 'GFE.jpg', title: 'Green Fungible Energy', category: 'Web3 / Crypto', description: 'A blockchain initiative to tokenize green energy — bridging environmental impact and economic incentive across ecosystem, NFT and community.', tech: ['React', 'Next.js', 'Solidity', 'Web3.js'], url: '' },
  { file: 'schwap.jpg', title: 'Schwap', category: 'DeFi', description: 'A minimalist Web3 dApp for a seed contribution and token swap, with connect-wallet, an ETH send input and terms / blueprint tabs.', tech: ['React', 'Solidity', 'ethers.js', 'wagmi'], url: '' },
  { file: 'solumberjack.jpg', title: 'So Lumberjack', category: 'Web3 / Crypto', description: 'A Solana devnet dApp demo letting users connect a wallet, request a 1 SOL airdrop and view their balance on the Solana stack.', tech: ['React', 'Rust', 'Anchor', 'web3.js'], url: '' },
  { file: 'woodpeckers-staking-solana.jpg', title: 'Blazin Woodpeckers', category: 'Staking dApp', description: 'A Solana NFT staking dApp for the Blazin Woodpeckers Genesis and Nest collections, with wallet selection and HadeSwap integration.', tech: ['React', 'Rust', 'Anchor', 'web3.js'], url: '' },
  { file: 'auto-trade-sand.jpg', title: 'Automated Trader', category: 'Trading Bot', description: 'A platform to track, compare and analyze trading activity with configurable webhook-based risk and order settings, on a live dashboard.', tech: ['React', 'Next.js', 'Node.js', 'WebSocket'], url: '' },
  { file: 'sky-watch.jpg', title: 'skyWatch', category: 'Dashboard', description: 'A weather dashboard showing current conditions and a temperature chart, with a three-day forecast plus humidity, pressure and wind.', tech: ['React', 'Chart.js', 'WeatherAPI'], url: '' },
  { file: 'bitematic.jpg', title: 'Bitematic', category: 'AI / SaaS', description: 'A restaurant solutions provider with online ordering, AI content creation and BiteBanter — a ChatGPT-powered chatbot for diners.', tech: ['React', 'Node.js', 'OpenAI API', 'MongoDB'], url: '' },
  { file: 'clientain.jpg', title: 'Clientain', category: 'AI / SaaS', description: 'A SaaS landing page for advanced conversational-AI that helps businesses deliver engaging customer and employee experiences.', tech: ['React', 'Next.js', 'TypeScript', 'Tailwind'], url: '' },
  { file: 'wizard-site.jpg', title: 'Wizard Web Group', category: 'Landing Page', description: 'A digital-agency landing page promoting cutting-edge web services, with order and demo CTAs and a Travigo travel-dashboard preview.', tech: ['React', 'Next.js', 'Tailwind', 'Framer Motion'], url: '' },
  { file: 'buefy-shop-pi.jpg', title: 'Buefy Shop', category: 'E-Commerce', description: 'An online clothing marketplace with a price-range filter, category selector and sale toggle, with add-to-cart across the catalog.', tech: ['Vue', 'Buefy', 'Node.js', 'Stripe'], url: '' },
  { file: 'hplus-sport-shop.jpg', title: 'H+ Sport Shop', category: 'E-Commerce', description: 'An online store for sportswear, supplements and flavored waters, with searchable listings, euro pricing and cart & share controls.', tech: ['Vue', 'Nuxt', 'Node.js', 'Stripe'], url: '' },
  { file: 'mishmash.jpg', title: 'mishmash', category: 'E-Commerce', description: 'A stationery store selling notebooks and notepads, with a bestseller log collection, planning layouts and a first-order discount.', tech: ['Vue', 'Nuxt', 'Shopify', 'Tailwind'], url: '' },
  { file: 'rosewoodpet.jpg', title: 'Rosewood Pet', category: 'E-Commerce', description: 'A pet-products catalog showcasing knock-down pet houses, bowls, toys and treats, with catalogue requests and stockist sign-up.', tech: ['Vue', 'Nuxt', 'Node.js', 'Stripe'], url: '' },
  { file: 'salinaka-ecommerce.jpg', title: 'Salinaka Eyewear', category: 'E-Commerce', description: 'An eyewear store selling glasses, sunglasses and contacts, with product search, featured listings and full account sign-up / sign-in.', tech: ['React', 'Redux', 'Firebase', 'Sass'], url: '' },
]

// ---- assemble pages → leaves -------------------------------------------
function chunk<T>(arr: T[], n: number): T[][] {
  const out: T[][] = []
  for (let i = 0; i < arr.length; i += n) out.push(arr.slice(i, i + n))
  return out
}
const projFaces = chunk(projects, 2).map((items, idx) => ({
  type: 'projects',
  folio: String(5 + idx).padStart(2, '0'),
  items,
}))
const faces: Record<string, any>[] = [
  { type: 'cover' },
  { type: 'inside' },
  { type: 'welcome', folio: '01' },
  { type: 'about', folio: '02' },
  { type: 'about2', folio: '03' },
  { type: 'workintro', folio: '04', count: projects.length },
  ...projFaces,
  { type: 'contactinfo', folio: String(5 + projFaces.length).padStart(2, '0') },
  { type: 'contactform', folio: String(6 + projFaces.length).padStart(2, '0') },
  { type: 'closing' },
]
// pair consecutive faces into leaves (front, back)
const leaves: { front: Record<string, any>; back: Record<string, any> | null }[] = []
for (let i = 0; i < faces.length; i += 2) {
  leaves.push({ front: faces[i], back: faces[i + 1] ?? null })
}
const N = leaves.length

const chapters = [
  { label: 'Cover', k: -1 },
  { label: 'Welcome', k: 0 },
  { label: 'About', k: 1 },
  { label: 'Work', k: 2 },
  { label: 'Contact', k: N - 2 },
]

function bgClass(face: Record<string, any> | null) {
  if (!face) return 'paper'
  if (face.type === 'cover') return 'cover'
  if (face.type === 'backcover') return 'cover back-cover'
  if (face.type === 'closing') return 'paper closing'
  return 'paper'
}

// ---- scroll → flip math ------------------------------------------------
const wrapper = ref<HTMLElement | null>(null)
const scroll = ref(0)
const vw = ref(1280)
const vh = ref(800)

const s = computed(() => scroll.value * N)
const open = computed(() => clamp(s.value / FLIP, 0, 1))
function leafT(i: number) {
  return clamp((s.value - i) / FLIP, 0, 1)
}
function leafStyle(i: number) {
  const t = leafT(i)
  const z = t <= 0 ? N - i : t >= 1 ? i : N + 5
  return { transform: `rotateY(${(-180 * t).toFixed(2)}deg)`, zIndex: z }
}

const scale = computed(() =>
  clamp(Math.min((vw.value - 48) / (PAGE_W * 2), (vh.value - 128) / PAGE_H), 0.32, 2.6)
)
const book3dStyle = computed(() => ({ height: PAGE_H + 'px', transform: `scale(${scale.value.toFixed(3)})` }))
const bookStyle = computed(() => ({
  width: PAGE_W + 'px',
  height: PAGE_H + 'px',
  transform: `translateX(${((open.value - 1) * 50).toFixed(2)}%)`,
}))

const currentLeaf = computed(() => (s.value < FLIP / 2 ? -1 : clamp(Math.round(s.value - 0.85), -1, N - 1)))
const activeK = computed(() => {
  let a = -1
  for (const c of chapters) if (c.k <= currentLeaf.value) a = c.k
  return a
})

let raf = 0
function measure() {
  vw.value = window.innerWidth
  vh.value = window.innerHeight
  update()
}
function update() {
  const el = wrapper.value
  if (!el) return
  const total = el.offsetHeight - window.innerHeight
  const passed = clamp(-el.getBoundingClientRect().top, 0, Math.max(total, 1))
  scroll.value = total > 0 ? passed / total : 0
}
function onScroll() {
  if (raf) return
  raf = requestAnimationFrame(() => { raf = 0; update() })
}
function goTo(k: number) {
  const el = wrapper.value
  if (!el) return
  const total = el.offsetHeight - window.innerHeight
  const target = k < 0 ? 0 : (k + 0.85) / N
  window.scrollTo({ top: el.offsetTop + target * total, behavior: 'smooth' })
}

onMounted(() => {
  measure()
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', measure)
})
onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('resize', measure)
  if (raf) cancelAnimationFrame(raf)
})
</script>

<template>
  <div ref="wrapper" class="book-wrapper" :style="{ height: `${(N + 1) * 100}vh` }">
    <div class="stage">
      <!-- top bar -->
      <div class="topbar">
        <button class="brand" @click="goTo(-1)">
          <span class="brand-mark"><img src="/logo-white.png" alt="Kato Himari logo" /></span>
          <span class="brand-name">Kato&nbsp;<b>Himari</b></span>
        </button>
        <nav class="chapters">
          <button
            v-for="c in chapters"
            :key="c.label"
            class="chip"
            :class="{ on: activeK === c.k }"
            @click="goTo(c.k)"
          >
            {{ c.label }}
          </button>
        </nav>
      </div>

      <!-- scaled stage -->
      <div class="book-3d" :style="book3dStyle">
        <div class="book" :style="bookStyle">
          <!-- static back cover (right side at the very end) -->
          <div class="leaf" :style="{ zIndex: 0 }">
            <div class="face front cover back-cover">
              <BookFace :face="{ type: 'backcover' }" side="front" />
            </div>
          </div>

          <!-- flipping leaves -->
          <div v-for="(leaf, i) in leaves" :key="i" class="leaf" :style="leafStyle(i)">
            <div class="face front" :class="bgClass(leaf.front)">
              <BookFace :face="leaf.front" side="front" @navigate="goTo" />
            </div>
            <div class="face back" :class="bgClass(leaf.back)">
              <BookFace v-if="leaf.back" :face="leaf.back" side="back" @navigate="goTo" />
            </div>
          </div>

          <div class="spine"></div>
        </div>
      </div>

      <!-- scroll hint -->
      <transition name="fade">
        <div v-if="scroll < 0.02" class="scroll-hint">
          <span>scroll</span>
          <Icon name="heroicons:chevron-down-20-solid" class="bob" />
        </div>
      </transition>
    </div>
  </div>
</template>

<style scoped>
.book-wrapper { position: relative; background: #06281f; }

.stage {
  position: sticky; top: 0; height: 100vh;
  display: flex; align-items: center; justify-content: center;
  overflow: hidden; perspective: 2400px; perspective-origin: 50% 46%;
  background: radial-gradient(120% 90% at 50% 8%, #0d4b3a 0%, #082c22 45%, #03130e 100%);
}
.stage::before {
  content: ''; position: absolute; width: 1100px; height: 1100px;
  background: radial-gradient(circle, rgba(16,185,129,0.18), transparent 60%);
  filter: blur(20px); pointer-events: none;
}

.book-3d { position: relative; transform-style: preserve-3d; }
.book {
  position: absolute; top: 0; left: 0; transform-style: preserve-3d;
  filter: drop-shadow(0 40px 60px rgba(0,0,0,0.55));
}
.leaf {
  position: absolute; inset: 0; transform-origin: left center;
  transform-style: preserve-3d; transition: transform 0.05s linear; will-change: transform;
}
.face {
  position: absolute; inset: 0; backface-visibility: hidden; -webkit-backface-visibility: hidden;
  overflow: hidden; border-radius: 4px 10px 10px 4px;
}
.face.back { transform: rotateY(180deg); }

.paper {
  background: linear-gradient(90deg, rgba(6,40,31,0.10), transparent 12%), linear-gradient(180deg, #fdfbf6, #f4efe4);
  color: #243029; box-shadow: inset 0 0 60px rgba(120,100,60,0.06);
}
.face.back.paper {
  background: linear-gradient(270deg, rgba(6,40,31,0.10), transparent 12%), linear-gradient(180deg, #fdfbf6, #f4efe4);
  border-radius: 10px 4px 4px 10px;
}
.closing { background: linear-gradient(180deg,#fdfbf6,#eef3ec) !important; }

.cover {
  background: radial-gradient(140% 120% at 20% 0%, #0c5a45 0%, #07412f 45%, #042a1f 100%);
  color: #eafff6; border-radius: 4px 12px 12px 4px;
  box-shadow: inset 0 0 0 1px rgba(255,255,255,0.06), inset 0 0 80px rgba(0,0,0,0.35);
}
.back-cover { border-radius: 4px 12px 12px 4px; }

.spine {
  position: absolute; top: 0; bottom: 0; left: -3px; width: 16px;
  background: linear-gradient(90deg, rgba(0,0,0,0.28), rgba(0,0,0,0));
  transform: translateZ(1px); pointer-events: none; z-index: 50;
}

/* chrome */
.topbar {
  position: absolute; top: 0; left: 0; right: 0; z-index: 60;
  display: flex; align-items: center; justify-content: space-between; padding: 18px 26px;
}
.brand { display: inline-flex; align-items: center; gap: 10px; background: none; border: none; cursor: pointer; color: #eafff6; }
.brand-mark { width: 40px; height: 32px; display: grid; place-items: center; }
.brand-mark img { width: 100%; height: 100%; object-fit: contain; object-position: left center; display: block; }
.brand-name { font: 500 16px/1 'Sora',sans-serif; color: #eafff6; }
.brand-name b { font-weight: 700; color: #6ee7b7; }
.chapters { display: flex; gap: 6px; background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.1); padding: 5px; border-radius: 999px; backdrop-filter: blur(8px); }
.chip { border: none; background: none; cursor: pointer; padding: 7px 13px; border-radius: 999px; font: 500 13px/1 'Inter',sans-serif; color: #bfe0d2; transition: all .2s; }
.chip:hover { color: #fff; }
.chip.on { background: #10b981; color: #04221a; font-weight: 600; }

.scroll-hint { position: absolute; bottom: 26px; left: 50%; transform: translateX(-50%); z-index: 60; display: flex; flex-direction: column; align-items: center; gap: 4px; color: #8fd3b9; font: 500 12px/1 'Inter',sans-serif; letter-spacing: .1em; }
.scroll-hint svg { width: 20px; height: 20px; }
.bob { animation: bob 1.6s ease-in-out infinite; }
@keyframes bob { 0%,100% { transform: translateY(0); } 50% { transform: translateY(5px); } }
.fade-enter-active,.fade-leave-active { transition: opacity .4s; }
.fade-enter-from,.fade-leave-to { opacity: 0; }

@media (max-width: 720px) { .chapters { display: none; } }
</style>
