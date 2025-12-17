# Christian Fea - Business Growth Strategist Website

A modern, responsive website redesign for Christian Fea built with Nuxt 3 and Tailwind CSS.

## Features

- Modern, professional design with smooth animations
- Fully responsive (mobile, tablet, desktop)
- SEO optimized with meta tags
- Fast performance with Nuxt 3 SSR/SSG
- Beautiful UI components with Tailwind CSS
- Icon support via @nuxt/icon

## Pages

- **Home** - Hero, Services, About, Testimonials, Blog preview, Contact sections
- **Services** - Detailed service offerings with process overview
- **About** - Personal story, values, and timeline
- **Blog** - Article listing with categories and individual post pages
- **Contact** - Contact form, scheduling, and FAQ

## Tech Stack

- **Framework**: Nuxt 3
- **Styling**: Tailwind CSS
- **Icons**: @nuxt/icon (Heroicons, MDI)
- **Fonts**: Inter, Playfair Display (Google Fonts)

## Setup

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Generate static site
npm run generate
```

## Project Structure

```
christian-fea-redesign/
├── assets/
│   └── css/
│       └── main.css          # Global styles & Tailwind config
├── components/
│   ├── AppHeader.vue         # Navigation header
│   ├── AppFooter.vue         # Site footer
│   └── sections/
│       ├── HeroSection.vue   # Homepage hero
│       ├── ServicesSection.vue
│       ├── AboutSection.vue
│       ├── TestimonialsSection.vue
│       ├── BlogSection.vue
│       ├── ContactSection.vue
│       └── CTASection.vue
├── layouts/
│   └── default.vue           # Main layout wrapper
├── pages/
│   ├── index.vue             # Homepage
│   ├── services.vue          # Services page
│   ├── about.vue             # About page
│   ├── contact.vue           # Contact page
│   └── blog/
│       ├── index.vue         # Blog listing
│       └── [slug].vue        # Individual blog posts
├── public/
│   ├── favicon.ico
│   └── grid.svg              # Background pattern
├── nuxt.config.ts            # Nuxt configuration
├── tailwind.config.js        # Tailwind configuration
└── package.json
```

## Customization

### Colors

The color palette is defined in `tailwind.config.js`:
- **Primary**: Blue (brand color)
- **Secondary**: Purple (accent)
- **Dark**: Slate gray (text/backgrounds)

### Fonts

- **Sans**: Inter (body text)
- **Display**: Playfair Display (headings)

### Components

All sections are modular Vue components that can be easily customized or reordered on any page.

## Next Steps (Recommendations)

1. **Connect to CMS**: Integrate with a headless CMS (Strapi, Contentful, Sanity) for blog posts
2. **Add Images**: Replace placeholder avatars/images with real photos
3. **Form Backend**: Connect contact form to email service (Formspree, SendGrid)
4. **Calendar Integration**: Add Calendly or Cal.com embed for scheduling
5. **Analytics**: Add Google Analytics or Plausible
6. **SEO**: Add sitemap and robots.txt generation

## License

Private - All rights reserved
