<script setup lang="ts">
/*
 * Renders the inner content of one book page (face), chosen by face.type.
 * The 3D leaf/face wrapper and page background live in BookExperience.vue;
 * this component only paints what's printed on the page.
 */
const props = defineProps<{
  face: Record<string, any>
  side: 'front' | 'back'
}>()
const emit = defineEmits<{
  (e: 'navigate', k: number): void
  (e: 'open', project: Record<string, any>): void
}>()

// folio sits on the outer edge: right pages are leaf fronts, left pages are backs
const folioRight = computed(() => props.side === 'front')

// self-contained mini contact form
const form = reactive({ name: '', email: '', message: '' })
const sent = ref(false)
function submit() {
  if (!form.name || !form.email) return
  sent.value = true
}

// typewriter that cycles through roles on the cover
const typed = ref('')
let timer: any = null
const roles = ['AI Full-Stack Developer', 'Web3 & Blockchain Engineer', 'Product-minded Builder']
let ri = 0
let ci = 0
let deleting = false
function tick() {
  const w = roles[ri]
  if (!deleting) {
    ci++
    typed.value = w.slice(0, ci)
    if (ci === w.length) { deleting = true; timer = setTimeout(tick, 1500); return }
  } else {
    ci--
    typed.value = w.slice(0, ci)
    if (ci === 0) { deleting = false; ri = (ri + 1) % roles.length }
  }
  timer = setTimeout(tick, deleting ? 38 : 78)
}
onMounted(() => { if (props.face.type === 'cover') tick() })
onUnmounted(() => { if (timer) clearTimeout(timer) })
</script>

<template>
  <!-- FRONT COVER -->
  <div v-if="face.type === 'cover'" class="cover-frame intro">
    <span class="cover-logo i1"><img src="/logo-white.png" alt="Kato Himari logo" /></span>
    <span class="cover-kicker i2">Portfolio · 2026</span>
    <h1 class="cover-title i3">Kato<br />Himari</h1>
    <div class="cover-rule i4"></div>
    <p class="cover-sub i5">{{ typed }}<span class="caret"></span></p>
    <span class="cover-open i6">
      <Icon name="heroicons:chevron-down-20-solid" class="bob" />
      scroll to open
    </span>
  </div>

  <!-- BACK COVER -->
  <div v-else-if="face.type === 'backcover'" class="cover-frame backcover-frame">
    <span class="cover-logo lg"><img src="/logo-white.png" alt="Kato Himari logo" /></span>
    <p class="cover-foot">Designed &amp; built by Kato Himari · AI Full-Stack Developer</p>
  </div>

  <!-- INSIDE COVER -->
  <div v-else-if="face.type === 'inside'" class="ph-pad center">
    <span class="folio">i</span>
    <span class="badge"><span class="dot"></span> Available for new projects</span>
    <p class="quote">“I design and build digital products where great engineering meets useful AI.”</p>
    <p class="muted">Turn the page to begin.</p>
  </div>

  <!-- WELCOME -->
  <div v-else-if="face.type === 'welcome'" class="ph-pad">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <span class="eyebrow">Welcome</span>
    <h2 class="h-lg">I turn complex ideas into products people <em>actually use</em>.</h2>
    <p class="lead">Web3 protocols, NFT marketplaces, DeFi dApps, AI tools and storefronts — I own
      the whole build: design, frontend, backend and the on-chain parts.</p>
    <div class="stats">
      <div><b>21</b><span>Projects</span></div>
      <div><b>10+</b><span>Years</span></div>
      <div><b>15+</b><span>Stacks</span></div>
    </div>
  </div>

  <!-- ABOUT (photo) -->
  <div v-else-if="face.type === 'about'" class="ph-pad">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <span class="eyebrow">About</span>
    <h2 class="h-md">Hi, I'm Kato.</h2>
    <div class="portrait">
      <img src="/Laks.png" alt="Kato Himari" />
      <span class="portrait-tag"><b>Kato Himari</b>AI Full-Stack Developer</span>
    </div>
  </div>

  <!-- ABOUT (strengths) -->
  <div v-else-if="face.type === 'about2'" class="ph-pad">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <p class="lead">I like the messy middle — a vague idea, a deadline, and shipping something
      solid at the end. I care about clean architecture, fast interfaces, and reaching for Web3
      or AI only when they genuinely make a product better.</p>
    <ul class="feature-list">
      <li>
        <Icon name="heroicons:code-bracket-20-solid" />
        <div><b>Full-Stack Engineering</b><span>React, Vue, Next.js, Node, Python.</span></div>
      </li>
      <li>
        <Icon name="heroicons:cube-transparent-20-solid" />
        <div><b>Web3 &amp; Blockchain</b><span>Solidity, Solana/Rust, ethers.js, dApps.</span></div>
      </li>
      <li>
        <Icon name="heroicons:cpu-chip-20-solid" />
        <div><b>AI Integration</b><span>OpenAI, Claude &amp; custom models.</span></div>
      </li>
    </ul>
  </div>

  <!-- WORK INTRO -->
  <div v-else-if="face.type === 'workintro'" class="ph-pad workintro">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <span class="eyebrow">Portfolio</span>
    <h2 class="h-lg">Selected<br />Work</h2>
    <p class="lead">{{ face.count }} products I've designed and shipped across Web3, DeFi, NFT
      platforms, AI tools and e-commerce. <b>Tap any card</b> for the story behind it.</p>
    <div class="legend">
      <span>DeFi</span><span>NFT</span><span>Web3</span><span>AI</span><span>E-Commerce</span>
    </div>
    <span class="turn-hint">keep scrolling to browse →</span>
  </div>

  <!-- PROJECTS GRID -->
  <div v-else-if="face.type === 'projects'" class="ph-pad projects">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <button
      v-for="p in face.items"
      :key="p.file"
      type="button"
      class="pcard"
      @click="emit('open', p)"
    >
      <div class="pshot"><img :src="`/portfolio/${p.file}`" :alt="p.title" loading="lazy" /></div>
      <div class="pmeta">
        <div class="prow">
          <span class="pcat">{{ p.category }}</span>
          <span class="pview">View case <Icon name="heroicons:arrow-right-20-solid" /></span>
        </div>
        <b class="ptitle">{{ p.title }}</b>
        <p class="pdesc">{{ p.description }}</p>
        <div class="ptags"><span v-for="t in p.tech.slice(0, 4)" :key="t">{{ t }}</span></div>
      </div>
    </button>
  </div>

  <!-- CONTACT INFO -->
  <div v-else-if="face.type === 'contactinfo'" class="ph-pad">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <span class="eyebrow">Contact</span>
    <h2 class="h-md">Let's work together.</h2>
    <ul class="contact-list">
      <li><Icon name="heroicons:envelope-20-solid" /> contact@katohimari.com</li>
      <li><Icon name="heroicons:calendar-20-solid" /> Free Q&amp;A — Wed @ 4PM PST</li>
      <li><Icon name="heroicons:map-pin-20-solid" /> Available worldwide</li>
    </ul>
    <div class="socials">
      <a href="#" aria-label="GitHub"><Icon name="mdi:github" /></a>
      <a href="#" aria-label="LinkedIn"><Icon name="mdi:linkedin" /></a>
      <a href="#" aria-label="Twitter"><Icon name="mdi:twitter" /></a>
    </div>
  </div>

  <!-- CONTACT FORM -->
  <div v-else-if="face.type === 'contactform'" class="ph-pad">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <h2 class="h-md">Start a project</h2>
    <form v-if="!sent" class="form" @submit.prevent="submit">
      <input v-model="form.name" type="text" placeholder="Your name" />
      <input v-model="form.email" type="email" placeholder="Email address" />
      <textarea v-model="form.message" rows="3" placeholder="Tell me about it…"></textarea>
      <button type="submit" class="send">Send message
        <Icon name="heroicons:paper-airplane-20-solid" />
      </button>
    </form>
    <div v-else class="thanks-mini">
      <Icon name="heroicons:check-circle-20-solid" />
      <p>Thanks, {{ form.name }} — I'll be in touch shortly.</p>
    </div>
  </div>

  <!-- CLOSING -->
  <div v-else-if="face.type === 'closing'" class="ph-pad center">
    <h2 class="h-lg">Thank you<br />for reading.</h2>
    <div class="cover-rule dark"></div>
    <p class="muted">Kato Himari — AI Full-Stack Developer</p>
    <button class="reopen" @click="emit('navigate', -1)">
      <Icon name="heroicons:arrow-up-20-solid" /> Back to cover
    </button>
  </div>
</template>

<style scoped>
.ph-pad { padding: 38px 36px; height: 100%; display: flex; flex-direction: column; gap: 13px; box-sizing: border-box; }
.ph-pad.center { align-items: center; justify-content: center; text-align: center; gap: 18px; }

.folio { position: absolute; top: 22px; left: 30px; font: 600 12px/1 'Cinzel', serif; letter-spacing: 0.2em; color: #a98f5d; }
.folio.r { left: auto; right: 30px; }

.eyebrow { font: 700 11px/1 'Cinzel', serif; letter-spacing: 0.3em; text-transform: uppercase; color: #2f6f5f; }
.h-lg { font: 700 40px/1.08 'Cinzel', serif; letter-spacing: -0.01em; color: #3a2c14; }
.h-md { font: 700 27px/1.12 'Cinzel', serif; letter-spacing: 0; color: #3a2c14; }
.h-lg em, .h-md em { color: #2f6f5f; font-style: italic; font-family: 'EB Garamond', serif; font-weight: 600; }
.lead { font: 400 16px/1.62 'EB Garamond', serif; color: #5b4a2c; }
.muted { color: #8a7546; font: 400 15px/1.6 'EB Garamond', serif; }

.stats { display: flex; gap: 24px; margin-top: auto; padding-top: 18px; border-top: 1px solid #cbb98e; }
.stats b { display: block; font: 700 28px/1 'Cinzel', serif; color: #2f6f5f; }
.stats span { font: 500 12px/1 'EB Garamond', serif; color: #97824f; }

.badge { display: inline-flex; align-items: center; gap: 8px; padding: 7px 14px; border: 1px solid #c8b485; border-radius: 999px; font: 600 12px/1 'EB Garamond', serif; color: #2f6f5f; background: rgba(70,120,105,0.12); }
.badge .dot { width: 8px; height: 8px; border-radius: 50%; background: #0f766e; box-shadow: 0 0 0 4px rgba(15,118,110,0.18); }
.quote { font: 500 23px/1.5 'Cinzel', serif; color: #46361b; max-width: 22ch; }

.portrait { position: relative; margin-top: auto; border-radius: 10px; overflow: hidden; aspect-ratio: 3/4; max-height: 62%; background: linear-gradient(135deg,#3a7d6e,#2f6f5f); padding: 4px; box-shadow: 0 10px 26px rgba(60,40,12,0.3); }
.portrait img { width: 100%; height: 100%; object-fit: cover; object-position: top center; border-radius: 7px; display: block; }
.portrait-tag { position: absolute; bottom: 14px; left: 14px; right: 14px; background: rgba(244,232,205,0.94); backdrop-filter: blur(4px); border-radius: 8px; padding: 10px 14px; font: 400 11px/1.3 'EB Garamond',serif; color: #7a673f; box-shadow: 0 8px 20px rgba(40,24,8,0.25); }
.portrait-tag b { display: block; font: 700 15px/1.2 'Cinzel',serif; color: #3a2c14; margin-bottom: 2px; }

.feature-list { list-style: none; padding: 0; margin: 6px 0 0; display: flex; flex-direction: column; gap: 16px; }
.feature-list li { display: flex; gap: 14px; align-items: flex-start; }
.feature-list svg { width: 26px; height: 26px; flex: none; color: #2f6f5f; background: rgba(70,120,105,0.16); padding: 5px; border-radius: 8px; box-sizing: content-box; }
.feature-list b { display: block; font: 600 15px/1.3 'Cinzel',serif; color: #3a2c14; }
.feature-list span { font: 400 13px/1.5 'EB Garamond',serif; color: #7a673f; }

/* work intro */
.workintro .legend { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 4px; }
.workintro .legend span { font: 600 11px/1 'Cinzel',serif; letter-spacing: .08em; text-transform: uppercase; color: #2f6f5f; background: rgba(70,120,105,0.12); border: 1px solid #cdb98a; padding: 6px 10px; border-radius: 999px; }
.turn-hint { margin-top: auto; font: 500 13px/1 'EB Garamond',serif; color: #a08a59; }

/* projects — 2 per page, full screenshot always visible (never cropped) */
.projects { gap: 14px; padding: 18px 26px; justify-content: center; }
.pcard { appearance: none; -webkit-appearance: none; font: inherit; text-align: left; width: 100%; padding: 0; cursor: pointer; display: flex; flex-direction: column; background: #f4ecda; border: 1px solid #c9beA0; border-radius: 8px; overflow: hidden; box-shadow: 0 6px 16px rgba(60,40,12,0.10); transition: transform .2s, box-shadow .2s, border-color .2s; }
.pcard:hover { transform: translateY(-2px); box-shadow: 0 14px 26px rgba(120,84,24,0.18); border-color: #b89a55; }
.pcard:hover .pview { opacity: 1; transform: translateX(0); }
.pcard:hover .pshot img { transform: scale(1.03); }
/* contain = the whole screenshot is always shown, never cropped */
.pshot { height: 152px; background: #e6ddc6; display: flex; align-items: center; justify-content: center; overflow: hidden; border-bottom: 1px solid #c9beA0; }
.pshot img { width: 100%; height: 100%; object-fit: contain; display: block; transition: transform .3s ease; }
.pmeta { padding: 11px 14px 13px; display: flex; flex-direction: column; gap: 4px; }
.prow { display: flex; align-items: center; justify-content: space-between; }
.pcat { font: 700 10px/1 'Cinzel',serif; letter-spacing: .14em; text-transform: uppercase; color: #2f6f5f; }
.pview { display: inline-flex; align-items: center; gap: 3px; font: 600 10px/1 'Cinzel',serif; color: #2f6f5f; opacity: 0; transform: translateX(-4px); transition: opacity .2s, transform .2s; }
.pview svg { width: 13px; height: 13px; }
.ptitle { font: 700 17px/1.2 'Cinzel',serif; color: #3a2c14; }
.pdesc { font: 400 12.5px/1.45 'EB Garamond',serif; color: #6f5c38; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
.ptags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 4px; }
.ptags span { font: 500 10px/1 'EB Garamond',serif; color: #3d5a4f; background: rgba(70,120,105,0.13); border: 1px solid #d8c79a; padding: 5px 8px; border-radius: 5px; }

/* contact */
.contact-list { list-style: none; padding: 0; margin: 4px 0; display: flex; flex-direction: column; gap: 13px; }
.contact-list li { display: flex; align-items: center; gap: 11px; font: 500 15px/1.3 'EB Garamond',serif; color: #4d3d20; }
.contact-list svg { width: 20px; height: 20px; color: #2f6f5f; }
.socials { display: flex; gap: 12px; margin-top: auto; }
.socials a { width: 42px; height: 42px; border-radius: 8px; background: #2c1c0c; color: #e8d4a4; display: flex; align-items: center; justify-content: center; transition: background .2s; }
.socials a:hover { background: #2f6f5f; color: #fff7e4; }
.socials svg { width: 20px; height: 20px; }

.form { display: flex; flex-direction: column; gap: 11px; margin-top: 6px; }
.form input, .form textarea { width: 100%; border: 1px solid #cab68a; border-radius: 7px; padding: 12px 14px; font: 400 15px/1.4 'EB Garamond',serif; color: #3a2c14; background: rgba(255,250,236,0.7); outline: none; resize: none; box-sizing: border-box; }
.form input:focus, .form textarea:focus { border-color: #3a7d6e; box-shadow: 0 0 0 3px rgba(184,146,63,0.18); }
.send { display: inline-flex; align-items: center; justify-content: center; gap: 8px; background: linear-gradient(180deg,#3a7d6e,#235e50); color: #f3eedd; border: none; border-radius: 7px; padding: 13px; font: 700 15px/1 'Cinzel',serif; cursor: pointer; }
.send svg { width: 18px; height: 18px; }
.thanks-mini { display: flex; flex-direction: column; align-items: center; gap: 12px; margin: auto; text-align: center; color: #2f6f5f; }
.thanks-mini svg { width: 46px; height: 46px; }
.thanks-mini p { font: 500 15px/1.5 'EB Garamond',serif; color: #4d3d20; }

/* covers */
.cover-frame { height: 100%; padding: 50px 44px; display: flex; flex-direction: column; justify-content: center; gap: 16px; border: 1px solid rgba(70,120,105,0.4); box-shadow: inset 0 0 0 4px rgba(70,120,105,0.10); margin: 18px; border-radius: 4px; box-sizing: border-box; }
.cover-logo { width: 116px; height: 92px; margin-bottom: 10px; }
.cover-logo img { width: 100%; height: 100%; object-fit: contain; object-position: left center; display: block; filter: drop-shadow(0 8px 22px rgba(0,0,0,0.45)); }
.cover-logo.lg { width: 150px; height: 118px; margin: 0 0 18px; }
.cover-logo.lg img { object-position: center; }
.cover-kicker { font: 600 12px/1 'Cinzel',serif; letter-spacing: .3em; text-transform: uppercase; color: #c9bf9f; }
.cover-title { font: 800 56px/0.98 'Cinzel',serif; letter-spacing: 0.01em; color: #ece3c8; text-shadow: 0 2px 10px rgba(0,0,0,0.4); }
.cover-rule { width: 70px; height: 2px; background: linear-gradient(90deg,#5fae98,#235e50); border-radius: 2px; }
.cover-rule.dark { background: linear-gradient(90deg,#3a7d6e,#235e50); }
.cover-sub { font: 400 19px/1.4 'EB Garamond',serif; font-style: italic; color: #cabf9f; min-height: 1.4em; }
.caret { display: inline-block; width: 2px; height: 1em; margin-left: 2px; vertical-align: -2px; background: #5fae98; animation: blink 1s steps(1) infinite; }
@keyframes blink { 50% { opacity: 0; } }

/* cover intro: staggered reveal on mount */
.intro > * { opacity: 0; animation: rise .7s cubic-bezier(.2,.7,.2,1) forwards; }
.intro .i1 { animation-delay: .05s; }
.intro .i2 { animation-delay: .18s; }
.intro .i3 { animation-delay: .30s; }
.intro .i4 { animation-delay: .44s; }
.intro .i5 { animation-delay: .56s; }
.intro .i6 { animation-delay: .80s; }
@keyframes rise { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
@media (prefers-reduced-motion: reduce) { .intro > * { opacity: 1; animation: none; } }
.cover-open { margin-top: auto; display: inline-flex; align-items: center; gap: 8px; font: 400 14px/1 'EB Garamond',serif; font-style: italic; color: #bcaf8a; letter-spacing: .05em; }
.cover-open svg { width: 18px; height: 18px; }
.backcover-frame { align-items: center; text-align: center; justify-content: center; }
.cover-foot { margin-top: auto; font: 400 13px/1.5 'EB Garamond',serif; font-style: italic; color: #b3a888; }
.reopen { margin-top: 4px; display: inline-flex; align-items: center; gap: 7px; background: #2c1c0c; color: #e8d4a4; border: 1px solid rgba(70,120,105,0.4); border-radius: 999px; padding: 11px 18px; font: 600 13px/1 'Cinzel',serif; cursor: pointer; }
.reopen svg { width: 16px; height: 16px; }

.bob { animation: bob 1.6s ease-in-out infinite; }
@keyframes bob { 0%,100% { transform: translateY(0); } 50% { transform: translateY(5px); } }
</style>
