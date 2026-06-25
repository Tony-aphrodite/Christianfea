<script setup lang="ts">
/*
 * Scroll-driven 3D book.
 * The whole portfolio is one book: scrolling opens the cover and turns each
 * leaf, revealing one section per spread. Page size is fixed (440x600) and the
 * spread is uniformly scaled to fit any viewport, so the layout never breaks.
 */

const N = 6                 // number of turnable leaves (cover + 5 content leaves)
const FLIP = 0.62           // fraction of each scroll-unit spent flipping (rest = dwell)
const PAGE_W = 440
const PAGE_H = 600

const clamp = (v: number, a: number, b: number) => Math.min(b, Math.max(a, v))

const wrapper = ref<HTMLElement | null>(null)
const scroll = ref(0)       // 0..1 progress through the book
const vw = ref(1280)
const vh = ref(800)

const chapters = [
  { label: 'Cover', k: -1 },
  { label: 'Welcome', k: 0 },
  { label: 'About', k: 1 },
  { label: 'Work', k: 2 },
  { label: 'Products', k: 3 },
  { label: 'Contact', k: 4 },
]

// reading head: how many leaves have begun turning
const s = computed(() => scroll.value * N)
const open = computed(() => clamp((s.value) / FLIP, 0, 1)) // cover-open amount

function leafT(i: number) {
  return clamp((s.value - i) / FLIP, 0, 1)
}
function leafStyle(i: number) {
  const t = leafT(i)
  const z = t <= 0 ? N - i : t >= 1 ? i : N + 5
  return {
    transform: `rotateY(${(-180 * t).toFixed(2)}deg)`,
    zIndex: z,
  }
}

// Grow the book to fill the viewport. It scales by whichever axis is the
// tighter fit (open spread width vs. height), and is allowed well past 1x so
// it gets large on big screens — text stays crisp because it's real DOM.
const scale = computed(() =>
  clamp(Math.min((vw.value - 48) / (PAGE_W * 2), (vh.value - 128) / PAGE_H), 0.32, 2.6)
)
const book3dStyle = computed(() => ({
  height: PAGE_H + 'px',
  transform: `scale(${scale.value.toFixed(3)})`,
}))
const bookStyle = computed(() => ({
  width: PAGE_W + 'px',
  height: PAGE_H + 'px',
  transform: `translateX(${((open.value - 1) * 50).toFixed(2)}%)`,
}))

const activeChapter = computed(() => {
  // which spread is currently most open
  if (s.value < FLIP / 2) return -1
  return clamp(Math.round(s.value - 0.8), -1, N - 1)
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
  raf = requestAnimationFrame(() => {
    raf = 0
    update()
  })
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

// mini contact form
const form = reactive({ name: '', email: '', message: '' })
const sent = ref(false)
function submit() {
  if (!form.name || !form.email) return
  sent.value = true
}
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
            :class="{ on: activeChapter === c.k }"
            @click="goTo(c.k)"
          >
            {{ c.label }}
          </button>
        </nav>
      </div>

      <!-- scaled stage -->
      <div class="book-3d" :style="book3dStyle">
        <div class="book" :style="bookStyle">
          <!-- back cover (static base, shows on the right at the end) -->
          <div class="leaf" :style="{ zIndex: 0 }">
            <div class="face front cover back-cover">
              <div class="cover-frame">
                <span class="cover-logo lg"><img src="/logo-white.png" alt="Kato Himari logo" /></span>
                <p class="cover-foot">Designed &amp; built by Kato Himari</p>
              </div>
            </div>
          </div>

          <!-- LEAF 0 — cover / inside cover -->
          <div class="leaf" :style="leafStyle(0)">
            <div class="face front cover">
              <div class="cover-frame">
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
            </div>
            <div class="face back paper">
              <span class="folio">i</span>
              <div class="ph-pad center">
                <span class="badge"><span class="dot"></span> Available for new projects</span>
                <p class="quote">“I design and build digital products where great engineering meets useful AI.”</p>
                <p class="muted">Turn the page to begin.</p>
              </div>
            </div>
          </div>

          <!-- LEAF 1 — welcome (right) / about (left) -->
          <div class="leaf" :style="leafStyle(1)">
            <div class="face front paper">
              <span class="folio r">01</span>
              <div class="ph-pad">
                <span class="eyebrow">Welcome</span>
                <h2 class="h-lg">Building digital products with <em>AI &amp; modern tech</em></h2>
                <p class="lead">I create scalable web &amp; mobile applications — from full-stack
                  platforms and automation systems to intelligent chatbots and APIs.</p>
                <div class="stats">
                  <div><b>10+</b><span>Years</span></div>
                  <div><b>50+</b><span>Projects</span></div>
                  <div><b>6+</b><span>Stacks</span></div>
                </div>
              </div>
            </div>
            <div class="face back paper">
              <span class="folio">02</span>
              <div class="ph-pad">
                <span class="eyebrow">About</span>
                <h2 class="h-md">A developer who ships, end to end.</h2>
                <div class="portrait">
                  <img src="/compressed_image.jpg" alt="Kato Himari" />
                  <span class="portrait-tag"><b>10+</b> yrs</span>
                </div>
              </div>
            </div>
          </div>

          <!-- LEAF 2 — about (right) / work (left) -->
          <div class="leaf" :style="leafStyle(2)">
            <div class="face front paper">
              <span class="folio r">03</span>
              <div class="ph-pad">
                <p class="lead">From concept to deployment, I take full ownership of the
                  development lifecycle — writing clean, maintainable code and integrating
                  AI where it genuinely helps.</p>
                <ul class="feature-list">
                  <li>
                    <Icon name="heroicons:code-bracket-20-solid" />
                    <div><b>Clean Architecture</b><span>Scalable, maintainable, modern frameworks.</span></div>
                  </li>
                  <li>
                    <Icon name="heroicons:cpu-chip-20-solid" />
                    <div><b>AI Integration</b><span>OpenAI, Claude &amp; custom models.</span></div>
                  </li>
                  <li>
                    <Icon name="heroicons:rocket-launch-20-solid" />
                    <div><b>End-to-End Delivery</b><span>Concept → design → deploy.</span></div>
                  </li>
                </ul>
              </div>
            </div>
            <div class="face back paper">
              <span class="folio">04</span>
              <div class="ph-pad">
                <span class="eyebrow">Selected Work</span>
                <h2 class="h-md">Things I've built.</h2>
                <div class="work">
                  <img src="/serve.png" alt="" />
                  <div>
                    <b>AI Automation for Growth</b>
                    <span>Workflow automation, chatbots &amp; API integrations.</span>
                    <em>PHP · Node.js · JavaScript</em>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- LEAF 3 — work (right) / products (left) -->
          <div class="leaf" :style="leafStyle(3)">
            <div class="face front paper">
              <span class="folio r">05</span>
              <div class="ph-pad">
                <div class="work">
                  <img src="/clothes.png" alt="" />
                  <div>
                    <b>Elegant Styles</b>
                    <span>Luxury fashion e-commerce platform.</span>
                    <em>Laravel · MySQL · Vue · AWS</em>
                  </div>
                </div>
                <div class="work">
                  <img src="/CRM.png" alt="" />
                  <div>
                    <b>AI Sales CRM</b>
                    <span>Lead management &amp; pipeline automation.</span>
                    <em>React · Next.js · Python · OpenAI</em>
                  </div>
                </div>
              </div>
            </div>
            <div class="face back paper">
              <span class="folio">06</span>
              <div class="ph-pad">
                <span class="eyebrow">Products</span>
                <h2 class="h-md">Live products.</h2>
                <a class="product" href="https://wolfandbadger.com" target="_blank" rel="noopener">
                  <span class="cat">Web App</span>
                  <b>E-Commerce Platform</b>
                  <span class="muted">Real-time inventory &amp; payments.</span>
                </a>
                <a class="product" href="https://poosting.com/" target="_blank" rel="noopener">
                  <span class="cat">Dashboard</span>
                  <b>Social Media Dashboard</b>
                  <span class="muted">Real-time analytics &amp; reporting.</span>
                </a>
              </div>
            </div>
          </div>

          <!-- LEAF 4 — products (right) / contact (left) -->
          <div class="leaf" :style="leafStyle(4)">
            <div class="face front paper">
              <span class="folio r">07</span>
              <div class="ph-pad">
                <a class="product" href="https://nomi.ai" target="_blank" rel="noopener">
                  <span class="cat">AI</span>
                  <b>AI-Powered Chatbot</b>
                  <span class="muted">NLP chatbot API for support automation.</span>
                </a>
                <p class="muted small">Each project is built with a production-ready stack and
                  shipped end to end. More available on request.</p>
              </div>
            </div>
            <div class="face back paper">
              <span class="folio">08</span>
              <div class="ph-pad">
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
            </div>
          </div>

          <!-- LEAF 5 — contact form (right) / closing (left) -->
          <div class="leaf" :style="leafStyle(5)">
            <div class="face front paper">
              <span class="folio r">09</span>
              <div class="ph-pad">
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
            </div>
            <div class="face back paper closing">
              <span class="folio">x</span>
              <div class="ph-pad center">
                <h2 class="h-lg">Thank you<br />for reading.</h2>
                <div class="cover-rule dark"></div>
                <p class="muted">Kato Himari — AI Full-Stack Developer</p>
                <button class="reopen" @click="goTo(-1)">
                  <Icon name="heroicons:arrow-up-20-solid" /> Back to cover
                </button>
              </div>
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
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  perspective: 2400px;
  perspective-origin: 50% 46%;
  background:
    radial-gradient(120% 90% at 50% 8%, #0d4b3a 0%, #082c22 45%, #03130e 100%);
}

/* ambient glow */
.stage::before {
  content: '';
  position: absolute;
  width: 1100px; height: 1100px;
  background: radial-gradient(circle, rgba(16,185,129,0.18), transparent 60%);
  filter: blur(20px);
  pointer-events: none;
}

.book-3d { position: relative; transform-style: preserve-3d; }

/* zero-width anchor: the book's left edge sits on the screen centre (the spine) */
.book {
  position: absolute;
  top: 0;
  left: 0;
  transform-style: preserve-3d;
  filter: drop-shadow(0 40px 60px rgba(0,0,0,0.55));
}

.leaf {
  position: absolute;
  inset: 0;
  transform-origin: left center;
  transform-style: preserve-3d;
  transition: transform 0.05s linear;
  will-change: transform;
}

.face {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  overflow: hidden;
  border-radius: 4px 10px 10px 4px;
}
.face.back { transform: rotateY(180deg); }

/* ---------- paper ---------- */
.paper {
  background:
    linear-gradient(90deg, rgba(6,40,31,0.10), transparent 12%),
    linear-gradient(180deg, #fdfbf6, #f4efe4);
  color: #243029;
  box-shadow: inset 0 0 60px rgba(120,100,60,0.06);
}
.face.back.paper {
  background:
    linear-gradient(270deg, rgba(6,40,31,0.10), transparent 12%),
    linear-gradient(180deg, #fdfbf6, #f4efe4);
  border-radius: 10px 4px 4px 10px;
}
.ph-pad { padding: 40px 38px; height: 100%; display: flex; flex-direction: column; gap: 14px; }
.ph-pad.center { align-items: center; justify-content: center; text-align: center; gap: 20px; }

.folio {
  position: absolute; top: 22px; left: 30px;
  font: 600 12px/1 'Sora', sans-serif; letter-spacing: 0.2em;
  color: #9bb7a8;
}
.folio.r { left: auto; right: 30px; }

.eyebrow {
  font: 700 11px/1 'Sora', sans-serif; letter-spacing: 0.28em; text-transform: uppercase;
  color: #059669;
}
.h-lg { font: 700 40px/1.05 'Sora', sans-serif; letter-spacing: -0.02em; color: #0f231b; }
.h-md { font: 700 28px/1.1 'Sora', sans-serif; letter-spacing: -0.01em; color: #0f231b; }
.h-lg em, .h-md em { color: #059669; font-style: normal; }
.lead { font: 400 16px/1.6 'Inter', sans-serif; color: #44544b; }
.muted { color: #7b8a80; font: 400 14px/1.6 'Inter', sans-serif; }
.muted.small { font-size: 13px; }

.stats { display: flex; gap: 26px; margin-top: auto; padding-top: 18px; border-top: 1px solid #e7e0d2; }
.stats b { display: block; font: 700 28px/1 'Sora', sans-serif; color: #047857; }
.stats span { font: 500 12px/1 'Inter', sans-serif; color: #8a978d; }

.badge {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 7px 14px; border: 1px solid #cfe6db; border-radius: 999px;
  font: 600 12px/1 'Inter', sans-serif; color: #047857; background: #f0faf5;
}
.badge .dot { width: 8px; height: 8px; border-radius: 50%; background: #10b981; box-shadow: 0 0 0 4px rgba(16,185,129,0.18); }
.quote { font: 500 22px/1.5 'Sora', sans-serif; color: #1f3327; max-width: 22ch; }

.portrait { position: relative; margin-top: auto; border-radius: 16px; overflow: hidden; aspect-ratio: 4/3; background: linear-gradient(135deg,#10b981,#047857); padding: 4px; }
.portrait img { width: 100%; height: 100%; object-fit: cover; border-radius: 13px; display: block; }
.portrait-tag { position: absolute; bottom: 14px; right: 14px; background: #fff; border-radius: 12px; padding: 8px 12px; font: 500 11px/1.2 'Inter',sans-serif; color: #6b7a70; box-shadow: 0 8px 20px rgba(0,0,0,0.15); }
.portrait-tag b { display: block; font: 700 18px/1 'Sora',sans-serif; color: #047857; }

.feature-list { list-style: none; padding: 0; margin: 6px 0 0; display: flex; flex-direction: column; gap: 16px; }
.feature-list li { display: flex; gap: 14px; align-items: flex-start; }
.feature-list svg { width: 26px; height: 26px; flex: none; color: #059669; background: #e7f7ef; padding: 5px; border-radius: 10px; box-sizing: content-box; }
.feature-list b { display: block; font: 600 15px/1.3 'Sora',sans-serif; color: #1f3327; }
.feature-list span { font: 400 13px/1.5 'Inter',sans-serif; color: #6b7a70; }

.work { display: flex; gap: 14px; align-items: center; background: #fff; border: 1px solid #ece5d7; border-radius: 14px; padding: 12px; box-shadow: 0 8px 18px rgba(60,50,20,0.05); }
.work + .work { margin-top: 14px; }
.work img { width: 84px; height: 64px; object-fit: cover; border-radius: 9px; flex: none; background: #e9efe9; }
.work b { display: block; font: 600 15px/1.3 'Sora',sans-serif; color: #1f3327; }
.work span { font: 400 12px/1.45 'Inter',sans-serif; color: #6b7a70; }
.work em { font: 500 11px/1 'Inter',sans-serif; color: #059669; font-style: normal; }

.product { display: block; background: #fff; border: 1px solid #ece5d7; border-left: 3px solid #10b981; border-radius: 12px; padding: 14px 16px; text-decoration: none; transition: transform .2s, box-shadow .2s; }
.product + .product { margin-top: 12px; }
.product:hover { transform: translateX(3px); box-shadow: 0 10px 22px rgba(5,150,105,0.12); }
.product .cat { font: 700 10px/1 'Sora',sans-serif; letter-spacing: .16em; text-transform: uppercase; color: #0d9488; }
.product b { display: block; margin: 5px 0 3px; font: 600 16px/1.2 'Sora',sans-serif; color: #1f3327; }

.contact-list { list-style: none; padding: 0; margin: 4px 0; display: flex; flex-direction: column; gap: 13px; }
.contact-list li { display: flex; align-items: center; gap: 11px; font: 500 14px/1.3 'Inter',sans-serif; color: #36463c; }
.contact-list svg { width: 20px; height: 20px; color: #059669; }
.socials { display: flex; gap: 12px; margin-top: auto; }
.socials a { width: 42px; height: 42px; border-radius: 12px; background: #0f231b; color: #d6efe4; display: flex; align-items: center; justify-content: center; transition: background .2s; }
.socials a:hover { background: #059669; color: #fff; }
.socials svg { width: 20px; height: 20px; }

.form { display: flex; flex-direction: column; gap: 11px; margin-top: 6px; }
.form input, .form textarea { width: 100%; border: 1px solid #d8d0bf; border-radius: 10px; padding: 12px 14px; font: 400 14px/1.4 'Inter',sans-serif; color: #243029; background: #fffdf8; outline: none; resize: none; }
.form input:focus, .form textarea:focus { border-color: #10b981; box-shadow: 0 0 0 3px rgba(16,185,129,0.15); }
.send { display: inline-flex; align-items: center; justify-content: center; gap: 8px; background: linear-gradient(90deg,#059669,#0d9488); color: #fff; border: none; border-radius: 10px; padding: 13px; font: 600 15px/1 'Sora',sans-serif; cursor: pointer; }
.send svg { width: 18px; height: 18px; }
.thanks-mini { display: flex; flex-direction: column; align-items: center; gap: 12px; margin: auto; text-align: center; color: #047857; }
.thanks-mini svg { width: 46px; height: 46px; }
.thanks-mini p { font: 500 15px/1.5 'Inter',sans-serif; color: #36463c; }

/* ---------- covers ---------- */
.cover {
  background:
    radial-gradient(140% 120% at 20% 0%, #0c5a45 0%, #07412f 45%, #042a1f 100%);
  color: #eafff6;
  border-radius: 4px 12px 12px 4px;
  box-shadow: inset 0 0 0 1px rgba(255,255,255,0.06), inset 0 0 80px rgba(0,0,0,0.35);
}
.cover-frame { height: 100%; padding: 50px 44px; display: flex; flex-direction: column; justify-content: center; gap: 16px; border: 1px solid rgba(212,239,228,0.16); margin: 18px; border-radius: 8px; }
.cover-logo { width: 116px; height: 92px; margin-bottom: 10px; }
.cover-logo img { width: 100%; height: 100%; object-fit: contain; object-position: left center; display: block; filter: drop-shadow(0 8px 22px rgba(0,0,0,0.35)); }
.cover-logo.lg { width: 150px; height: 118px; margin: 0 0 18px; }
.cover-logo.lg img { object-position: center; }
.cover-kicker { font: 600 12px/1 'Sora',sans-serif; letter-spacing: .3em; text-transform: uppercase; color: #6ee7b7; }
.cover-title { font: 800 56px/0.98 'Sora',sans-serif; letter-spacing: -0.02em; }
.cover-rule { width: 64px; height: 3px; background: linear-gradient(90deg,#34d399,#0d9488); border-radius: 2px; }
.cover-rule.dark { background: linear-gradient(90deg,#059669,#0d9488); }
.cover-sub { font: 400 18px/1.4 'Inter',sans-serif; color: #b7d8cb; }
.cover-open { margin-top: auto; display: inline-flex; align-items: center; gap: 8px; font: 500 13px/1 'Inter',sans-serif; color: #8fd3b9; letter-spacing: .05em; }
.cover-open svg { width: 18px; height: 18px; }
.back-cover { border-radius: 4px 12px 12px 4px; }
.back-cover .cover-frame { align-items: center; text-align: center; justify-content: center; gap: 0; }
.cover-mono { margin-top: auto; font: 700 22px/1 'Sora',sans-serif; letter-spacing: .3em; color: #6ee7b7; }
.cover-foot { margin-top: auto; font: 400 12px/1.5 'Inter',sans-serif; color: #7fb9a3; }
.closing { background: linear-gradient(180deg,#fdfbf6,#eef3ec); }
.reopen { margin-top: 4px; display: inline-flex; align-items: center; gap: 7px; background: #0f231b; color: #d6efe4; border: none; border-radius: 999px; padding: 11px 18px; font: 600 13px/1 'Sora',sans-serif; cursor: pointer; }
.reopen svg { width: 16px; height: 16px; }

/* spine shadow that sits over the gutter */
.spine {
  position: absolute; top: 0; bottom: 0; left: -3px; width: 16px;
  background: linear-gradient(90deg, rgba(0,0,0,0.28), rgba(0,0,0,0));
  transform: translateZ(1px);
  pointer-events: none; z-index: 50;
}

/* ---------- chrome ---------- */
.topbar {
  position: absolute; top: 0; left: 0; right: 0; z-index: 60;
  display: flex; align-items: center; justify-content: space-between;
  padding: 18px 26px;
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

@media (max-width: 720px) {
  .chapters { display: none; }
}
</style>
