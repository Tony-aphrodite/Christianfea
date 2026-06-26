<script setup lang="ts">
/*
 * Scroll-driven 3D book. Scrolling opens the cover and turns each leaf, one
 * spread at a time. Page content is data-driven and rendered by <BookFace>.
 * This file owns the 3D mechanics, page realism (turn shading, thickness,
 * spine progress, ribbon, sound), keyboard nav and the case-study modal.
 */
const clamp = (v: number, a: number, b: number) => Math.min(b, Math.max(a, v))
const PAGE_W = 440
const PAGE_H = 600
const FLIP = 0.62

// ---- portfolio data (edit me) ------------------------------------------
const projects = [
  { file: 'Axelar.JPG', title: 'Axelar', category: 'Cross-Chain', url: '', description: 'A cross-chain interoperability network letting institutions like Citi, Deutsche Bank and Mastercard navigate a secure multichain world.', tech: ['React', 'Next.js', 'Solidity', 'Go'], challenge: 'Communicate deep cross-chain infrastructure to both developers and enterprise partners on a single, credible marketing site.', highlights: ['Component-driven Next.js marketing site', 'Animated cross-chain network & flow visuals', 'CMS-driven partner, docs and ecosystem sections', 'Tuned for fast global loads and SEO'], outcome: 'A polished front door used to build trust with institutional partners.' },
  { file: 'ternoa.jpg', title: 'Ternoa', category: 'Web3 / Crypto', url: '', description: 'Landing site for an evolutionary NFT blockchain — private content, delegation, renting, validators and staking.', tech: ['React', 'Next.js', 'Rust', 'Polkadot.js'], challenge: 'Explain an “evolutionary NFT” chain and its many features without overwhelming first-time visitors.', highlights: ['Feature sections for private content, delegation & renting', 'Validator and token-economy pages with data viz', 'Reusable scroll-reveal animation system', 'Fully responsive multi-section landing'], outcome: 'A clear narrative that made the protocol’s NFT features easy to grasp.' },
  { file: 'tofunft.jpg', title: 'tofuNFT', category: 'NFT Marketplace', url: 'tofunft.com', description: 'A multi-chain NFT marketplace on BNB Chain with collection banners, a mint launchpad and live trending collections.', tech: ['React', 'Next.js', 'Solidity', 'ethers.js'], challenge: 'Deliver a fast marketplace that browses many collections across chains with live on-chain activity.', highlights: ['Collection, item & launchpad pages on on-chain data', 'Wallet connection and multi-chain switching', 'Trending/hot collections with live sales feeds', 'Reusable card grid + filtering for large catalogs'], outcome: 'A smooth multi-chain browsing experience with a live mint launchpad.' },
  { file: 'Creaticles.JPG', title: 'Creaticles', category: 'NFT Marketplace', url: '', description: 'A Web3 platform for NFT contests where users post requests and submit artwork, with USDT, ETH and FTM prize pools.', tech: ['React', 'Next.js', 'Solidity', 'IPFS'], highlights: ['NFT contest creation & submission flows', 'Wallet connect with multi-token prize pools', 'IPFS artwork uploads & on-chain settlement'] },
  { file: 'iZUMi.png', title: 'iZUMi Finance', category: 'DeFi', url: '', description: 'A multi-chain DeFi protocol delivering programmable liquidity-as-a-service and concentrated liquidity market-making.', tech: ['React', 'Next.js', 'Solidity', 'TypeScript'], highlights: ['UI for concentrated liquidity & LaaS', 'Multi-chain network switching', 'Real-time pool & position data'] },
  { file: 'Localcryptos.JPG', title: 'LocalCoinSwap', category: 'Web3 / Crypto', url: '', description: 'A non-custodial peer-to-peer crypto exchange supporting buy, sell, swap and cash trading with private-key access.', tech: ['Vue', 'Django', 'Python', 'Web3.js'], highlights: ['Non-custodial P2P trading flows', 'Buy / sell / swap / cash-trade UIs', 'Private-key based account access'] },
  { file: 'reefscan.jpg', title: 'ReefScan', category: 'Web3 / Crypto', url: '', description: 'A Reef blockchain explorer for searching blocks, accounts, transfers and contracts, with live network stats.', tech: ['React', 'GraphQL', 'Polkadot.js', 'TypeScript'], highlights: ['Block / account / contract explorer search', 'Live network-stat dashboards', 'GraphQL-powered data tables'] },
  { file: 'GFE.jpg', title: 'Green Fungible Energy', category: 'Web3 / Crypto', url: '', description: 'A blockchain initiative to tokenize green energy — bridging environmental impact and economic incentive.', tech: ['React', 'Next.js', 'Solidity', 'Web3.js'], highlights: ['Tokenized green-energy landing', 'Ecosystem, NFT & community sections', 'Wallet connect + token info'] },
  { file: 'schwap.jpg', title: 'Schwap', category: 'DeFi', url: '', description: 'A minimalist Web3 dApp for a seed contribution and token swap, with connect-wallet and an ETH send flow.', tech: ['React', 'Solidity', 'ethers.js', 'wagmi'], highlights: ['Minimal swap & seed-contribution dApp', 'Connect wallet + ETH send flow', 'Terms / blueprint tabbed UI'] },
  { file: 'solumberjack.jpg', title: 'So Lumberjack', category: 'Web3 / Crypto', url: '', description: 'A Solana devnet dApp demo letting users connect a wallet, request a 1 SOL airdrop and view their balance.', tech: ['React', 'Rust', 'Anchor', 'web3.js'], highlights: ['Solana devnet wallet connection', '1 SOL airdrop request flow', 'Live balance display'] },
  { file: 'woodpeckers-staking-solana.jpg', title: 'Blazin Woodpeckers', category: 'Staking dApp', url: '', description: 'A Solana NFT staking dApp for the Blazin Woodpeckers Genesis and Nest collections, with HadeSwap integration.', tech: ['React', 'Rust', 'Anchor', 'web3.js'], highlights: ['Solana NFT staking dApp', 'Genesis & Nest collection support', 'HadeSwap partner integration'] },
  { file: 'auto-trade-sand.jpg', title: 'Automated Trader', category: 'Trading Bot', url: '', description: 'A platform to track, compare and analyze trading activity with configurable webhook-based risk and order settings.', tech: ['React', 'Next.js', 'Node.js', 'WebSocket'], highlights: ['Live trading-activity dashboard', 'Webhook-based risk / order config', 'Compare & analyze views'] },
  { file: 'sky-watch.jpg', title: 'skyWatch', category: 'Dashboard', url: '', description: 'A weather dashboard showing current conditions and a temperature chart, with a three-day forecast.', tech: ['React', 'Chart.js', 'WeatherAPI'], highlights: ['Current conditions + 3-day forecast', 'Temperature chart with Chart.js', 'Humidity / pressure / wind readouts'] },
  { file: 'bitematic.jpg', title: 'Bitematic', category: 'AI / SaaS', url: '', description: 'A restaurant solutions provider with online ordering, AI content creation and a ChatGPT-powered chatbot.', tech: ['React', 'Node.js', 'OpenAI API', 'MongoDB'], highlights: ['Online ordering for restaurants', 'AI content-generation tools', 'BiteBanter ChatGPT chatbot'] },
  { file: 'clientain.jpg', title: 'Clientain', category: 'AI / SaaS', url: '', description: 'A SaaS landing page for advanced conversational-AI that helps businesses deliver engaging experiences.', tech: ['React', 'Next.js', 'TypeScript', 'Tailwind'], highlights: ['Conversational-AI SaaS landing', 'Feature & use-case sections', 'Lead capture & CTAs'] },
  { file: 'wizard-site.jpg', title: 'Wizard Web Group', category: 'Landing Page', url: '', description: 'A digital-agency landing page promoting web services, with order/demo CTAs and a Travigo dashboard preview.', tech: ['React', 'Next.js', 'Tailwind', 'Framer Motion'], highlights: ['Agency landing with bold motion', 'Order & demo CTAs', 'Travigo dashboard preview'] },
  { file: 'buefy-shop-pi.jpg', title: 'Buefy Shop', category: 'E-Commerce', url: '', description: 'An online clothing marketplace with a price-range filter, category selector and sale toggle.', tech: ['Vue', 'Buefy', 'Node.js', 'Stripe'], highlights: ['Clothing marketplace UI', 'Price / category / sale filters', 'Cart & checkout flow'] },
  { file: 'hplus-sport-shop.jpg', title: 'H+ Sport Shop', category: 'E-Commerce', url: '', description: 'An online store for sportswear, supplements and flavored waters, with searchable listings and euro pricing.', tech: ['Vue', 'Nuxt', 'Node.js', 'Stripe'], highlights: ['Sportswear & supplements store', 'Searchable catalog, euro pricing', 'Cart & share controls'] },
  { file: 'mishmash.jpg', title: 'mishmash', category: 'E-Commerce', url: '', description: 'A stationery store selling notebooks and notepads, with a bestseller collection and a first-order discount.', tech: ['Vue', 'Nuxt', 'Shopify', 'Tailwind'], highlights: ['Stationery e-commerce', 'Bestseller collections', 'First-order discount capture'] },
  { file: 'rosewoodpet.jpg', title: 'Rosewood Pet', category: 'E-Commerce', url: '', description: 'A pet-products catalog showcasing pet houses, bowls, toys and treats, with catalogue and stockist sign-up.', tech: ['Vue', 'Nuxt', 'Node.js', 'Stripe'], highlights: ['Pet products catalog', 'Catalogue request & stockist signup', 'Clean product browsing'] },
  { file: 'salinaka-ecommerce.jpg', title: 'Salinaka Eyewear', category: 'E-Commerce', url: '', description: 'An eyewear store selling glasses, sunglasses and contacts, with product search and account sign-up.', tech: ['React', 'Redux', 'Firebase', 'Sass'], highlights: ['Eyewear store (glasses / contacts)', 'Product search & featured items', 'Account sign-up / sign-in'] },
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
const leaves: { front: Record<string, any>; back: Record<string, any> | null }[] = []
for (let i = 0; i < faces.length; i += 2) leaves.push({ front: faces[i], back: faces[i + 1] ?? null })
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
const prog = computed(() => clamp(s.value / N, 0, 1))
function leafT(i: number) {
  return clamp((s.value - i) / FLIP, 0, 1)
}
function leafStyle(i: number) {
  const t = leafT(i)
  const z = t <= 0 ? N - i : t >= 1 ? i : N + 5
  return { transform: `rotateY(${(-180 * t).toFixed(2)}deg)`, zIndex: z }
}
// dynamic turn shading: a page darkens as it rotates away from the reader
function frontShade(i: number) { return (leafT(i) * 0.6).toFixed(3) }
function backShade(i: number) { return ((1 - leafT(i)) * 0.55).toFixed(3) }

const scale = computed(() =>
  clamp(Math.min((vw.value - 48) / (PAGE_W * 2), (vh.value - 128) / PAGE_H), 0.32, 2.6)
)
const book3dStyle = computed(() => ({ height: PAGE_H + 'px', transform: `scale(${scale.value.toFixed(3)})` }))
const bookStyle = computed(() => ({
  width: PAGE_W + 'px',
  height: PAGE_H + 'px',
  transform: `translateX(${((open.value - 1) * 50).toFixed(2)}%)`,
}))
const EDGE = 18
const blockRightStyle = computed(() => ({ width: Math.max(2, (1 - prog.value) * EDGE).toFixed(1) + 'px' }))
const blockLeftStyle = computed(() => ({ width: Math.max(0, prog.value * EDGE).toFixed(1) + 'px' }))

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

// ---- page-turn sound (synthesized, opt-in) -----------------------------
const sound = ref(false)
let actx: AudioContext | null = null
function toggleSound() {
  sound.value = !sound.value
  if (sound.value && !actx) {
    const AC = (window as any).AudioContext || (window as any).webkitAudioContext
    if (AC) actx = new AC()
  }
  actx?.resume?.()
}
function playTurn() {
  if (!sound.value || !actx) return
  const ctx = actx
  const dur = 0.16
  const buffer = ctx.createBuffer(1, Math.floor(ctx.sampleRate * dur), ctx.sampleRate)
  const data = buffer.getChannelData(0)
  for (let i = 0; i < data.length; i++) {
    const t = i / data.length
    data[i] = (Math.random() * 2 - 1) * Math.pow(1 - t, 2.2)
  }
  const src = ctx.createBufferSource(); src.buffer = buffer
  const bp = ctx.createBiquadFilter(); bp.type = 'bandpass'; bp.frequency.value = 2400; bp.Q.value = 0.6
  const g = ctx.createGain(); g.gain.value = 0.16
  src.connect(bp); bp.connect(g); g.connect(ctx.destination)
  src.start()
}
watch(currentLeaf, playTurn)

// ---- keyboard navigation ----------------------------------------------
const selected = ref<Record<string, any> | null>(null)
function openProject(p: Record<string, any>) { selected.value = p }
function visit(url: string) { return 'https://' + url.replace(/^https?:\/\//, '') }
function onKey(e: KeyboardEvent) {
  if (selected.value) { if (e.key === 'Escape') selected.value = null; return }
  if (e.key === 'ArrowRight' || e.key === 'PageDown') { e.preventDefault(); goTo(Math.min(currentLeaf.value + 1, N - 1)) }
  else if (e.key === 'ArrowLeft' || e.key === 'PageUp') { e.preventDefault(); goTo(Math.max(currentLeaf.value - 1, -1)) }
}

onMounted(() => {
  measure()
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', measure)
  window.addEventListener('keydown', onKey)
})
onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('resize', measure)
  window.removeEventListener('keydown', onKey)
  if (raf) cancelAnimationFrame(raf)
})
</script>

<template>
  <div ref="wrapper" class="book-wrapper" :style="{ height: `${(N + 1) * 100}vh` }">
    <div class="stage">
      <!-- ambient layers -->
      <div class="aurora"></div>
      <div class="stars"></div>

      <!-- top bar -->
      <div class="topbar">
        <button class="brand" @click="goTo(-1)">
          <span class="brand-mark"><img src="/logo-white.png" alt="Kato Himari logo" /></span>
          <span class="brand-name">Kato&nbsp;<b>Himari</b></span>
        </button>
        <div class="topright">
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
          <button class="snd" :class="{ on: sound }" :title="sound ? 'Sound on' : 'Sound off'" @click="toggleSound">
            <Icon :name="sound ? 'heroicons:speaker-wave-20-solid' : 'heroicons:speaker-x-mark-20-solid'" />
          </button>
        </div>
      </div>

      <!-- scaled stage -->
      <div class="book-3d" :style="book3dStyle">
        <div class="book" :style="bookStyle">
          <!-- page-stack thickness (fore-edges) -->
          <div class="block block-right" :style="blockRightStyle"></div>
          <div class="block block-left" :style="blockLeftStyle"></div>

          <!-- static back cover (right side at the very end) -->
          <div class="leaf" :style="{ zIndex: 0 }">
            <div class="face front cover back-cover">
              <BookFace :face="{ type: 'backcover' }" side="front" />
            </div>
          </div>

          <!-- flipping leaves -->
          <div v-for="(leaf, i) in leaves" :key="i" class="leaf" :style="leafStyle(i)">
            <div class="face front" :class="bgClass(leaf.front)">
              <BookFace :face="leaf.front" side="front" @navigate="goTo" @open="openProject" />
              <i class="shade" :style="{ opacity: frontShade(i) }"></i>
            </div>
            <div class="face back" :class="bgClass(leaf.back)">
              <BookFace v-if="leaf.back" :face="leaf.back" side="back" @navigate="goTo" @open="openProject" />
              <i class="shade" :style="{ opacity: backShade(i) }"></i>
            </div>
          </div>

          <!-- gutter shadow + reading progress on the spine -->
          <div class="spine"></div>
          <div class="read-bar" :style="{ height: (prog * 100).toFixed(1) + '%' }"></div>

          <!-- bookmark ribbon -->
          <button class="ribbon" title="Jump to contact" @click="goTo(N - 2)">
            <span class="ribbon-label">Contact</span>
          </button>
        </div>
      </div>

      <!-- scroll hint -->
      <transition name="fade">
        <div v-if="scroll < 0.02" class="scroll-hint">
          <span>scroll · or use ← →</span>
          <Icon name="heroicons:chevron-down-20-solid" class="bob" />
        </div>
      </transition>
    </div>

    <!-- case-study modal -->
    <transition name="cs">
      <div v-if="selected" class="cs-overlay" @click.self="selected = null">
        <div class="cs">
          <button class="cs-close" @click="selected = null"><Icon name="heroicons:x-mark-20-solid" /></button>
          <div class="cs-shot"><img :src="`/portfolio/${selected.file}`" :alt="selected.title" /></div>
          <div class="cs-body">
            <span class="cs-cat">{{ selected.category }}</span>
            <h3 class="cs-title">{{ selected.title }}</h3>
            <p class="cs-desc">{{ selected.description }}</p>

            <template v-if="selected.challenge">
              <h4 class="cs-h">Challenge</h4>
              <p class="cs-p">{{ selected.challenge }}</p>
              <h4 class="cs-h">What I built</h4>
              <ul class="cs-list"><li v-for="h in selected.highlights" :key="h">{{ h }}</li></ul>
              <h4 class="cs-h">Outcome</h4>
              <p class="cs-p">{{ selected.outcome }}</p>
            </template>
            <template v-else-if="selected.highlights">
              <h4 class="cs-h">Highlights</h4>
              <ul class="cs-list"><li v-for="h in selected.highlights" :key="h">{{ h }}</li></ul>
            </template>

            <div class="cs-tags"><span v-for="t in selected.tech" :key="t">{{ t }}</span></div>
            <a v-if="selected.url" class="cs-visit" :href="visit(selected.url)" target="_blank" rel="noopener">
              Visit site <Icon name="heroicons:arrow-up-right-20-solid" />
            </a>
          </div>
        </div>
      </div>
    </transition>
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
/* ambient aurora that slowly drifts */
.aurora {
  position: absolute; inset: -20%; pointer-events: none; opacity: 0.5; mix-blend-mode: screen;
  background:
    radial-gradient(40% 30% at 20% 30%, rgba(52,211,153,0.25), transparent 60%),
    radial-gradient(35% 28% at 80% 25%, rgba(13,148,136,0.25), transparent 60%),
    radial-gradient(45% 35% at 60% 80%, rgba(16,185,129,0.18), transparent 60%);
  filter: blur(40px); animation: drift 22s ease-in-out infinite alternate;
}
@keyframes drift { 0% { transform: translate3d(-3%, -2%, 0) scale(1); } 100% { transform: translate3d(4%, 3%, 0) scale(1.1); } }
/* sparse twinkling star field */
.stars {
  position: absolute; inset: 0; pointer-events: none;
  background-image:
    radial-gradient(1px 1px at 12% 22%, rgba(255,255,255,0.8), transparent),
    radial-gradient(1px 1px at 28% 68%, rgba(255,255,255,0.6), transparent),
    radial-gradient(1.5px 1.5px at 47% 14%, rgba(255,255,255,0.7), transparent),
    radial-gradient(1px 1px at 63% 52%, rgba(255,255,255,0.6), transparent),
    radial-gradient(1px 1px at 78% 30%, rgba(255,255,255,0.7), transparent),
    radial-gradient(1.5px 1.5px at 88% 72%, rgba(255,255,255,0.6), transparent),
    radial-gradient(1px 1px at 38% 88%, rgba(255,255,255,0.6), transparent);
  animation: twinkle 5s ease-in-out infinite alternate;
}
@keyframes twinkle { 0% { opacity: 0.35; } 100% { opacity: 0.8; } }

.book-3d { position: relative; transform-style: preserve-3d; }
.book { position: absolute; top: 0; left: 0; transform-style: preserve-3d; filter: drop-shadow(0 40px 60px rgba(0,0,0,0.55)); }

/* page-stack thickness on the fore-edges */
.block { position: absolute; top: 6px; bottom: 6px; z-index: 1; border-radius: 2px;
  background: repeating-linear-gradient(to bottom, #f3ede0 0, #f3ede0 2px, #d9cfb9 2px, #d9cfb9 3px); }
.block-right { left: 100%; transform: translateX(-2px); box-shadow: 2px 0 6px rgba(0,0,0,0.25); border-radius: 0 3px 3px 0; }
.block-left { right: 100%; transform: translateX(2px); box-shadow: -2px 0 6px rgba(0,0,0,0.25); border-radius: 3px 0 0 3px; }

.leaf { position: absolute; inset: 0; transform-origin: left center; transform-style: preserve-3d; transition: transform 0.05s linear; will-change: transform; }
.face { position: absolute; inset: 0; backface-visibility: hidden; -webkit-backface-visibility: hidden; overflow: hidden; border-radius: 4px 10px 10px 4px; }
.face.back { transform: rotateY(180deg); }
/* dynamic turn shading overlay */
.shade { position: absolute; inset: 0; pointer-events: none; z-index: 40;
  background: linear-gradient(100deg, rgba(0,0,0,0) 35%, rgba(0,0,0,0.5) 100%); }
.face.back .shade { background: linear-gradient(260deg, rgba(0,0,0,0) 35%, rgba(0,0,0,0.5) 100%); }

.paper { background: linear-gradient(90deg, rgba(6,40,31,0.10), transparent 12%), linear-gradient(180deg, #fdfbf6, #f4efe4); color: #243029; box-shadow: inset 0 0 60px rgba(120,100,60,0.06); }
.face.back.paper { background: linear-gradient(270deg, rgba(6,40,31,0.10), transparent 12%), linear-gradient(180deg, #fdfbf6, #f4efe4); border-radius: 10px 4px 4px 10px; }
.closing { background: linear-gradient(180deg,#fdfbf6,#eef3ec) !important; }
.cover { background: radial-gradient(140% 120% at 20% 0%, #0c5a45 0%, #07412f 45%, #042a1f 100%); color: #eafff6; border-radius: 4px 12px 12px 4px; box-shadow: inset 0 0 0 1px rgba(255,255,255,0.06), inset 0 0 80px rgba(0,0,0,0.35); }
.back-cover { border-radius: 4px 12px 12px 4px; }

.spine { position: absolute; top: 0; bottom: 0; left: -3px; width: 16px; background: linear-gradient(90deg, rgba(0,0,0,0.28), rgba(0,0,0,0)); transform: translateZ(1px); pointer-events: none; z-index: 50; }
.read-bar { position: absolute; top: 0; left: -1px; width: 3px; background: linear-gradient(180deg,#34d399,#0d9488); box-shadow: 0 0 8px rgba(52,211,153,0.7); border-radius: 2px; transform: translateZ(2px); z-index: 51; pointer-events: none; }

/* bookmark ribbon */
.ribbon { position: absolute; top: -10px; right: 46px; width: 30px; height: 120px; border: none; cursor: pointer; padding: 0; z-index: 52;
  background: linear-gradient(180deg,#10b981,#047857); box-shadow: 0 6px 14px rgba(0,0,0,0.35);
  clip-path: polygon(0 0, 100% 0, 100% 100%, 50% 82%, 0 100%); transform: translateZ(3px); transition: height .25s ease; }
.ribbon:hover { height: 138px; }
.ribbon-label { position: absolute; top: 30px; left: 50%; transform: translateX(-50%) rotate(90deg); transform-origin: center; white-space: nowrap; font: 700 10px/1 'Sora',sans-serif; letter-spacing: .14em; text-transform: uppercase; color: #eafff6; }

/* chrome */
.topbar { position: absolute; top: 0; left: 0; right: 0; z-index: 60; display: flex; align-items: center; justify-content: space-between; padding: 18px 26px; }
.topright { display: flex; align-items: center; gap: 10px; }
.brand { display: inline-flex; align-items: center; gap: 10px; background: none; border: none; cursor: pointer; color: #eafff6; }
.brand-mark { width: 40px; height: 32px; display: grid; place-items: center; }
.brand-mark img { width: 100%; height: 100%; object-fit: contain; object-position: left center; display: block; }
.brand-name { font: 500 16px/1 'Sora',sans-serif; color: #eafff6; }
.brand-name b { font-weight: 700; color: #6ee7b7; }
.chapters { display: flex; gap: 6px; background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.1); padding: 5px; border-radius: 999px; backdrop-filter: blur(8px); }
.chip { border: none; background: none; cursor: pointer; padding: 7px 13px; border-radius: 999px; font: 500 13px/1 'Inter',sans-serif; color: #bfe0d2; transition: all .2s; }
.chip:hover { color: #fff; }
.chip.on { background: #10b981; color: #04221a; font-weight: 600; }
.snd { width: 38px; height: 38px; border-radius: 999px; display: grid; place-items: center; cursor: pointer; color: #bfe0d2; background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.1); transition: all .2s; }
.snd:hover { color: #fff; }
.snd.on { background: #10b981; color: #04221a; border-color: transparent; }
.snd svg { width: 18px; height: 18px; }

.scroll-hint { position: absolute; bottom: 26px; left: 50%; transform: translateX(-50%); z-index: 60; display: flex; flex-direction: column; align-items: center; gap: 4px; color: #8fd3b9; font: 500 12px/1 'Inter',sans-serif; letter-spacing: .1em; }
.scroll-hint svg { width: 20px; height: 20px; }
.bob { animation: bob 1.6s ease-in-out infinite; }
@keyframes bob { 0%,100% { transform: translateY(0); } 50% { transform: translateY(5px); } }
.fade-enter-active,.fade-leave-active { transition: opacity .4s; }
.fade-enter-from,.fade-leave-to { opacity: 0; }

/* case-study modal */
.cs-overlay { position: fixed; inset: 0; z-index: 200; display: flex; align-items: center; justify-content: center; padding: 24px; background: rgba(3,16,12,0.74); backdrop-filter: blur(6px); }
.cs { position: relative; width: min(680px, 96vw); max-height: 90vh; overflow: hidden; display: flex; flex-direction: column; background: #0c2b22; border: 1px solid rgba(110,231,183,0.18); border-radius: 18px; box-shadow: 0 40px 90px rgba(0,0,0,0.6); }
.cs-close { position: absolute; top: 12px; right: 12px; z-index: 2; width: 36px; height: 36px; border-radius: 999px; border: none; cursor: pointer; background: rgba(0,0,0,0.4); color: #eafff6; display: grid; place-items: center; }
.cs-close svg { width: 20px; height: 20px; }
.cs-shot { background: #081c16; max-height: 300px; overflow: hidden; display: flex; align-items: center; justify-content: center; }
.cs-shot img { width: 100%; height: 100%; object-fit: contain; max-height: 300px; display: block; }
.cs-body { padding: 24px 28px 28px; overflow-y: auto; color: #d7ece3; }
.cs-cat { font: 700 11px/1 'Sora',sans-serif; letter-spacing: .16em; text-transform: uppercase; color: #34d399; }
.cs-title { font: 700 26px/1.1 'Sora',sans-serif; color: #fff; margin: 8px 0 10px; }
.cs-desc { font: 400 15px/1.6 'Inter',sans-serif; color: #bcd6cb; }
.cs-h { font: 700 12px/1 'Sora',sans-serif; letter-spacing: .12em; text-transform: uppercase; color: #6ee7b7; margin: 20px 0 8px; }
.cs-p { font: 400 14px/1.6 'Inter',sans-serif; color: #bcd6cb; }
.cs-list { margin: 0; padding: 0; list-style: none; display: flex; flex-direction: column; gap: 8px; }
.cs-list li { position: relative; padding-left: 20px; font: 400 14px/1.5 'Inter',sans-serif; color: #cfe6db; }
.cs-list li::before { content: ''; position: absolute; left: 2px; top: 8px; width: 7px; height: 7px; border-radius: 50%; background: #10b981; }
.cs-tags { display: flex; flex-wrap: wrap; gap: 7px; margin-top: 20px; }
.cs-tags span { font: 500 11px/1 'Inter',sans-serif; color: #9fe4c9; background: rgba(16,185,129,0.12); border: 1px solid rgba(16,185,129,0.25); padding: 6px 9px; border-radius: 7px; }
.cs-visit { display: inline-flex; align-items: center; gap: 7px; margin-top: 22px; background: linear-gradient(90deg,#059669,#0d9488); color: #fff; text-decoration: none; padding: 12px 18px; border-radius: 10px; font: 600 14px/1 'Sora',sans-serif; }
.cs-visit svg { width: 16px; height: 16px; }
.cs-enter-active,.cs-leave-active { transition: opacity .25s; }
.cs-enter-from,.cs-leave-to { opacity: 0; }
.cs-enter-active .cs,.cs-leave-active .cs { transition: transform .25s ease; }
.cs-enter-from .cs,.cs-leave-to .cs { transform: translateY(16px) scale(0.98); }

@media (max-width: 720px) { .chapters { display: none; } }
</style>
