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
const emit = defineEmits<{ (e: 'navigate', k: number): void }>()

// folio sits on the outer edge: right pages are leaf fronts, left pages are backs
const folioRight = computed(() => props.side === 'front')

// self-contained mini contact form
const form = reactive({ name: '', email: '', message: '' })
const sent = ref(false)
function submit() {
  if (!form.name || !form.email) return
  sent.value = true
}
function href(url: string) {
  return url ? 'https://' + url.replace(/^https?:\/\//, '') : undefined
}
</script>

<template>
  <!-- FRONT COVER -->
  <div v-if="face.type === 'cover'" class="cover-frame">
    <span class="cover-logo"><img src="/logo-white.png" alt="Kato Himari logo" /></span>
    <span class="cover-kicker">Portfolio · 2026</span>
    <h1 class="cover-title">Kato<br />Himari</h1>
    <div class="cover-rule"></div>
    <p class="cover-sub">AI Full-Stack Developer</p>
    <span class="cover-open">
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
    <h2 class="h-lg">Building digital products with <em>AI &amp; modern tech</em></h2>
    <p class="lead">I create scalable web &amp; mobile applications — from full-stack platforms
      and Web3 dApps to automation systems, intelligent chatbots and APIs.</p>
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
    <p class="lead">I take full ownership of the development lifecycle — from concept and design
      to deployment — writing clean, maintainable code and bringing Web3 and AI to life where
      they genuinely add value.</p>
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
    <p class="lead">A selection of {{ face.count }} shipped products across Web3, DeFi, NFT
      platforms, AI tools and e-commerce.</p>
    <div class="legend">
      <span>DeFi</span><span>NFT</span><span>Web3</span><span>AI</span><span>E-Commerce</span>
    </div>
    <span class="turn-hint">keep scrolling to browse →</span>
  </div>

  <!-- PROJECTS GRID -->
  <div v-else-if="face.type === 'projects'" class="ph-pad projects">
    <span class="folio" :class="{ r: folioRight }">{{ face.folio }}</span>
    <a
      v-for="p in face.items"
      :key="p.file"
      class="pcard"
      :class="{ link: !!p.url }"
      :href="href(p.url)"
      :target="p.url ? '_blank' : undefined"
      rel="noopener"
    >
      <div class="pshot"><img :src="`/portfolio/${p.file}`" :alt="p.title" loading="lazy" /></div>
      <div class="pmeta">
        <div class="prow">
          <span class="pcat">{{ p.category }}</span>
          <Icon v-if="p.url" name="heroicons:arrow-up-right-20-solid" class="pext" />
        </div>
        <b class="ptitle">{{ p.title }}</b>
        <p class="pdesc">{{ p.description }}</p>
        <div class="ptags"><span v-for="t in p.tech.slice(0, 4)" :key="t">{{ t }}</span></div>
      </div>
    </a>
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

.folio { position: absolute; top: 22px; left: 30px; font: 600 12px/1 'Sora', sans-serif; letter-spacing: 0.2em; color: #9bb7a8; }
.folio.r { left: auto; right: 30px; }

.eyebrow { font: 700 11px/1 'Sora', sans-serif; letter-spacing: 0.28em; text-transform: uppercase; color: #059669; }
.h-lg { font: 700 40px/1.05 'Sora', sans-serif; letter-spacing: -0.02em; color: #0f231b; }
.h-md { font: 700 27px/1.1 'Sora', sans-serif; letter-spacing: -0.01em; color: #0f231b; }
.h-lg em, .h-md em { color: #059669; font-style: normal; }
.lead { font: 400 15px/1.6 'Inter', sans-serif; color: #44544b; }
.muted { color: #7b8a80; font: 400 14px/1.6 'Inter', sans-serif; }

.stats { display: flex; gap: 24px; margin-top: auto; padding-top: 18px; border-top: 1px solid #e7e0d2; }
.stats b { display: block; font: 700 28px/1 'Sora', sans-serif; color: #047857; }
.stats span { font: 500 12px/1 'Inter', sans-serif; color: #8a978d; }

.badge { display: inline-flex; align-items: center; gap: 8px; padding: 7px 14px; border: 1px solid #cfe6db; border-radius: 999px; font: 600 12px/1 'Inter', sans-serif; color: #047857; background: #f0faf5; }
.badge .dot { width: 8px; height: 8px; border-radius: 50%; background: #10b981; box-shadow: 0 0 0 4px rgba(16,185,129,0.18); }
.quote { font: 500 22px/1.5 'Sora', sans-serif; color: #1f3327; max-width: 22ch; }

.portrait { position: relative; margin-top: auto; border-radius: 16px; overflow: hidden; aspect-ratio: 3/4; max-height: 62%; background: linear-gradient(135deg,#10b981,#047857); padding: 4px; }
.portrait img { width: 100%; height: 100%; object-fit: cover; object-position: top center; border-radius: 13px; display: block; }
.portrait-tag { position: absolute; bottom: 14px; left: 14px; right: 14px; background: rgba(255,255,255,0.92); backdrop-filter: blur(4px); border-radius: 12px; padding: 10px 14px; font: 400 11px/1.3 'Inter',sans-serif; color: #6b7a70; box-shadow: 0 8px 20px rgba(0,0,0,0.18); }
.portrait-tag b { display: block; font: 700 15px/1.2 'Sora',sans-serif; color: #0f231b; margin-bottom: 2px; }

.feature-list { list-style: none; padding: 0; margin: 6px 0 0; display: flex; flex-direction: column; gap: 16px; }
.feature-list li { display: flex; gap: 14px; align-items: flex-start; }
.feature-list svg { width: 26px; height: 26px; flex: none; color: #059669; background: #e7f7ef; padding: 5px; border-radius: 10px; box-sizing: content-box; }
.feature-list b { display: block; font: 600 15px/1.3 'Sora',sans-serif; color: #1f3327; }
.feature-list span { font: 400 13px/1.5 'Inter',sans-serif; color: #6b7a70; }

/* work intro */
.workintro .legend { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 4px; }
.workintro .legend span { font: 600 11px/1 'Sora',sans-serif; letter-spacing: .08em; text-transform: uppercase; color: #0d9488; background: #effaf6; border: 1px solid #d3ece2; padding: 6px 10px; border-radius: 999px; }
.turn-hint { margin-top: auto; font: 500 13px/1 'Inter',sans-serif; color: #93a399; }

/* projects — 2 per page, full screenshot always visible (never cropped) */
.projects { gap: 14px; padding: 18px 26px; justify-content: center; }
.pcard { display: flex; flex-direction: column; background: #fff; border: 1px solid #ece5d7; border-radius: 14px; overflow: hidden; text-decoration: none; box-shadow: 0 6px 16px rgba(60,50,20,0.05); transition: transform .2s, box-shadow .2s, border-color .2s; }
.pcard.link:hover { transform: translateY(-2px); box-shadow: 0 14px 26px rgba(5,150,105,0.14); border-color: #b9e3d2; }
/* contain = the whole screenshot is always shown, never cropped */
.pshot { height: 152px; background: #eef0ec; display: flex; align-items: center; justify-content: center; overflow: hidden; border-bottom: 1px solid #ece5d7; }
.pshot img { width: 100%; height: 100%; object-fit: contain; display: block; }
.pmeta { padding: 11px 14px 13px; display: flex; flex-direction: column; gap: 4px; }
.prow { display: flex; align-items: center; justify-content: space-between; }
.pcat { font: 700 10px/1 'Sora',sans-serif; letter-spacing: .14em; text-transform: uppercase; color: #0d9488; }
.pext { width: 16px; height: 16px; color: #94a99e; }
.ptitle { font: 700 16px/1.2 'Sora',sans-serif; color: #1f3327; }
.pdesc { font: 400 12px/1.45 'Inter',sans-serif; color: #6b7a70; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
.ptags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 4px; }
.ptags span { font: 500 10px/1 'Inter',sans-serif; color: #4d7a68; background: #eef7f2; border: 1px solid #dcefe5; padding: 5px 8px; border-radius: 6px; }

/* contact */
.contact-list { list-style: none; padding: 0; margin: 4px 0; display: flex; flex-direction: column; gap: 13px; }
.contact-list li { display: flex; align-items: center; gap: 11px; font: 500 14px/1.3 'Inter',sans-serif; color: #36463c; }
.contact-list svg { width: 20px; height: 20px; color: #059669; }
.socials { display: flex; gap: 12px; margin-top: auto; }
.socials a { width: 42px; height: 42px; border-radius: 12px; background: #0f231b; color: #d6efe4; display: flex; align-items: center; justify-content: center; transition: background .2s; }
.socials a:hover { background: #059669; color: #fff; }
.socials svg { width: 20px; height: 20px; }

.form { display: flex; flex-direction: column; gap: 11px; margin-top: 6px; }
.form input, .form textarea { width: 100%; border: 1px solid #d8d0bf; border-radius: 10px; padding: 12px 14px; font: 400 14px/1.4 'Inter',sans-serif; color: #243029; background: #fffdf8; outline: none; resize: none; box-sizing: border-box; }
.form input:focus, .form textarea:focus { border-color: #10b981; box-shadow: 0 0 0 3px rgba(16,185,129,0.15); }
.send { display: inline-flex; align-items: center; justify-content: center; gap: 8px; background: linear-gradient(90deg,#059669,#0d9488); color: #fff; border: none; border-radius: 10px; padding: 13px; font: 600 15px/1 'Sora',sans-serif; cursor: pointer; }
.send svg { width: 18px; height: 18px; }
.thanks-mini { display: flex; flex-direction: column; align-items: center; gap: 12px; margin: auto; text-align: center; color: #047857; }
.thanks-mini svg { width: 46px; height: 46px; }
.thanks-mini p { font: 500 15px/1.5 'Inter',sans-serif; color: #36463c; }

/* covers */
.cover-frame { height: 100%; padding: 50px 44px; display: flex; flex-direction: column; justify-content: center; gap: 16px; border: 1px solid rgba(212,239,228,0.16); margin: 18px; border-radius: 8px; box-sizing: border-box; }
.cover-logo { width: 116px; height: 92px; margin-bottom: 10px; }
.cover-logo img { width: 100%; height: 100%; object-fit: contain; object-position: left center; display: block; filter: drop-shadow(0 8px 22px rgba(0,0,0,0.35)); }
.cover-logo.lg { width: 150px; height: 118px; margin: 0 0 18px; }
.cover-logo.lg img { object-position: center; }
.cover-kicker { font: 600 12px/1 'Sora',sans-serif; letter-spacing: .3em; text-transform: uppercase; color: #6ee7b7; }
.cover-title { font: 800 56px/0.98 'Sora',sans-serif; letter-spacing: -0.02em; color: #eafff6; }
.cover-rule { width: 64px; height: 3px; background: linear-gradient(90deg,#34d399,#0d9488); border-radius: 2px; }
.cover-rule.dark { background: linear-gradient(90deg,#059669,#0d9488); }
.cover-sub { font: 400 18px/1.4 'Inter',sans-serif; color: #b7d8cb; }
.cover-open { margin-top: auto; display: inline-flex; align-items: center; gap: 8px; font: 500 13px/1 'Inter',sans-serif; color: #8fd3b9; letter-spacing: .05em; }
.cover-open svg { width: 18px; height: 18px; }
.backcover-frame { align-items: center; text-align: center; justify-content: center; }
.cover-foot { margin-top: auto; font: 400 12px/1.5 'Inter',sans-serif; color: #7fb9a3; }
.reopen { margin-top: 4px; display: inline-flex; align-items: center; gap: 7px; background: #0f231b; color: #d6efe4; border: none; border-radius: 999px; padding: 11px 18px; font: 600 13px/1 'Sora',sans-serif; cursor: pointer; }
.reopen svg { width: 16px; height: 16px; }

.bob { animation: bob 1.6s ease-in-out infinite; }
@keyframes bob { 0%,100% { transform: translateY(0); } 50% { transform: translateY(5px); } }
</style>
