# Performance Standards

## Overview

Web performance directly impacts user experience, SEO rankings, and conversion rates. This guide focuses on Google's Core Web Vitals, the official metrics that Google uses as ranking factors.

**Why performance matters:**
- **User experience** - Fast sites feel professional and trustworthy
- **SEO rankings** - Core Web Vitals are official Google ranking factors (since June 2021)
- **Conversions** - Amazon found every 100ms of latency costs 1% in revenue
- **Bounce rate** - 53% of mobile users abandon sites that take over 3 seconds to load
- **Mobile users** - Performance is even more critical on slower connections

**Performance targets:**
- **Core Web Vitals:** GREEN on all three metrics
- **PageSpeed Insights score:** 90+ (desktop), 80+ (mobile)
- **Lighthouse Performance score:** 90+
- **Time to Interactive:** < 3.8 seconds
- **Total page size:** < 2 MB

## Core Web Vitals

Google's Core Web Vitals are three specific metrics that measure loading, interactivity, and visual stability. These are official ranking factors.

### LCP (Largest Contentful Paint)

**What it measures:** Loading performance - how long until the main content is visible.

**Specifically:** Time until the largest image or text block in the viewport is rendered.

**Targets:**
- **Good:** < 2.5 seconds (GREEN)
- **Needs improvement:** 2.5 - 4.0 seconds (YELLOW)
- **Poor:** > 4.0 seconds (RED)

**What counts as LCP element:**
- `<img>` elements
- `<image>` elements inside `<svg>`
- `<video>` elements (poster image)
- Background images loaded via `url()`
- Block-level elements containing text nodes

**Common LCP elements:**
- Hero images
- Banner images
- Large text blocks (H1)
- Video thumbnails
- Full-width content images

#### LCP Optimization Strategies

**1. Optimize images (biggest impact)**
```html
<!-- ✅ Optimized hero image -->
<img
  src="hero-image.webp"
  alt="Professional plumbing service"
  width="1200"
  height="600"
  fetchpriority="high"
  decoding="async"
>
```

**Key techniques:**
- **Format:** Use WebP (20-30% smaller than JPG)
- **Compression:** Compress images (aim for 100-200 KB for hero images)
- **Dimensions:** Serve correctly sized images (don't scale down)
- **Fetch priority:** Add `fetchpriority="high"` to LCP image
- **Preload:** Preload LCP image if it's not in initial HTML

```html
<!-- Preload LCP image (if loaded via CSS or lazy-loaded) -->
<link rel="preload" as="image" href="hero-image.webp" fetchpriority="high">
```

**2. Remove render-blocking resources**
```html
<!-- ❌ Render-blocking CSS -->
<link rel="stylesheet" href="styles.css">

<!-- ✅ Inline critical CSS, defer non-critical -->
<style>
  /* Critical above-the-fold CSS inlined here */
  .hero { ... }
  .nav { ... }
</style>

<!-- Load non-critical CSS asynchronously -->
<link rel="preload" href="non-critical.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="non-critical.css"></noscript>
```

**3. Minimize JavaScript execution**
```html
<!-- ❌ Render-blocking JavaScript -->
<script src="app.js"></script>

<!-- ✅ Defer JavaScript -->
<script src="app.js" defer></script>

<!-- ✅ Or async (if order doesn't matter) -->
<script src="analytics.js" async></script>
```

**4. Optimize server response time**
- **Target:** < 600ms TTFB (Time to First Byte)
- **Use CDN:** Cloudflare Pages serves from edge locations
- **Static generation:** Astro pre-renders HTML (no server processing)
- **Caching:** Set proper cache headers

**5. Avoid lazy-loading LCP element**
```html
<!-- ❌ Don't lazy-load hero image -->
<img src="hero.jpg" loading="lazy" alt="Hero">

<!-- ✅ Hero image loads immediately -->
<img src="hero.jpg" alt="Hero" fetchpriority="high">

<!-- ✅ Below-the-fold images lazy-load -->
<img src="below-fold.jpg" loading="lazy" alt="Content">
```

#### LCP Common Issues & Fixes

**Issue: Large image file size**
- **Fix:** Compress images, use WebP format
- **Tool:** Squoosh.app, ImageOptim, TinyPNG

**Issue: Slow server response**
- **Fix:** Use CDN (Cloudflare), static site generation (Astro)
- **Test:** WebPageTest TTFB

**Issue: Render-blocking CSS/JS**
- **Fix:** Inline critical CSS, defer JavaScript
- **Tool:** Chrome DevTools Coverage tab

**Issue: Client-side rendering**
- **Fix:** Use SSG (Static Site Generation) instead of CSR
- **Astro benefit:** Static generation by default

### FID/INP (First Input Delay / Interaction to Next Paint)

**FID (deprecated March 2024, replaced by INP):**
- **What it measured:** Time from first user interaction to browser response
- **Target:** < 100ms

**INP (new metric as of March 2024):**
- **What it measures:** Responsiveness - how quickly page responds to ALL user interactions
- **Specifically:** Worst-case interaction delay throughout page lifecycle

**Targets:**
- **Good:** < 200ms (GREEN)
- **Needs improvement:** 200 - 500ms (YELLOW)
- **Poor:** > 500ms (RED)

**What counts as interaction:**
- Clicks
- Taps
- Keyboard presses

**What INP measures:**
- Input delay (time to start processing)
- Processing time (running event handlers)
- Presentation delay (rendering updates)

#### INP Optimization Strategies

**1. Minimize JavaScript execution**
```javascript
// ❌ Heavy synchronous processing
function handleClick() {
  const data = processLargeDataset(); // Blocks main thread
  updateUI(data);
}

// ✅ Break up long tasks
async function handleClick() {
  const data = await processInChunks();
  requestIdleCallback(() => updateUI(data));
}

// ✅ Use Web Workers for heavy computation
const worker = new Worker('process-worker.js');
worker.postMessage(largeDataset);
worker.onmessage = (e) => updateUI(e.data);
```

**2. Debounce expensive operations**
```javascript
// ❌ Run on every keystroke
input.addEventListener('input', (e) => {
  expensiveSearchFunction(e.target.value);
});

// ✅ Debounce to reduce calls
import { debounce } from 'lodash-es';

const debouncedSearch = debounce((value) => {
  expensiveSearchFunction(value);
}, 300);

input.addEventListener('input', (e) => {
  debouncedSearch(e.target.value);
});
```

**3. Optimize event handlers**
```javascript
// ❌ Heavy work in event handler
button.addEventListener('click', () => {
  // 500ms of synchronous work
  performComplexCalculation();
  updateMultipleElements();
  triggerAnimations();
});

// ✅ Optimize and break up work
button.addEventListener('click', () => {
  // Immediate feedback
  button.classList.add('loading');

  // Defer heavy work
  requestIdleCallback(() => {
    performComplexCalculation();
  });

  // Batch DOM updates
  requestAnimationFrame(() => {
    updateMultipleElements();
    triggerAnimations();
  });
});
```

**4. Code splitting**
```javascript
// ❌ Load everything upfront
import { heavyLibrary } from 'heavy-library';

// ✅ Dynamic import when needed
button.addEventListener('click', async () => {
  const { heavyLibrary } = await import('heavy-library');
  heavyLibrary.doSomething();
});
```

**5. Reduce third-party script impact**
```html
<!-- ❌ Synchronous third-party script -->
<script src="https://example.com/widget.js"></script>

<!-- ✅ Async loading -->
<script src="https://example.com/widget.js" async></script>

<!-- ✅ Or defer -->
<script src="https://example.com/widget.js" defer></script>

<!-- ✅ Load on interaction (even better) -->
<script>
  button.addEventListener('click', () => {
    const script = document.createElement('script');
    script.src = 'https://example.com/widget.js';
    document.head.appendChild(script);
  }, { once: true });
</script>
```

#### INP Common Issues & Fixes

**Issue: Large JavaScript bundles**
- **Fix:** Code splitting, tree shaking, remove unused code
- **Tool:** webpack-bundle-analyzer, Chrome DevTools Coverage

**Issue: Long tasks (> 50ms)**
- **Fix:** Break up into smaller tasks, use requestIdleCallback
- **Tool:** Chrome DevTools Performance tab

**Issue: Third-party scripts blocking main thread**
- **Fix:** Load async, defer, or on user interaction
- **Tool:** Chrome DevTools Performance tab

**Issue: Heavy event handlers**
- **Fix:** Debounce, throttle, or optimize logic
- **Tool:** Chrome DevTools Performance profiling

### CLS (Cumulative Layout Shift)

**What it measures:** Visual stability - how much content shifts unexpectedly during loading.

**Specifically:** Sum of all unexpected layout shift scores throughout page lifecycle.

**Targets:**
- **Good:** < 0.1 (GREEN)
- **Needs improvement:** 0.1 - 0.25 (YELLOW)
- **Poor:** > 0.25 (RED)

**What causes layout shifts:**
- Images without dimensions
- Ads/embeds/iframes without dimensions
- Dynamically injected content
- Web fonts causing FOIT/FOUT
- Animations moving existing content

#### CLS Optimization Strategies

**1. Always specify image dimensions**
```html
<!-- ❌ No dimensions (causes layout shift when image loads) -->
<img src="photo.jpg" alt="Photo">

<!-- ✅ Explicit width/height (reserves space) -->
<img
  src="photo.jpg"
  alt="Photo"
  width="800"
  height="600"
  loading="lazy"
>

<!-- ✅ Aspect ratio with CSS (responsive) -->
<img
  src="photo.jpg"
  alt="Photo"
  style="aspect-ratio: 16/9; width: 100%; height: auto;"
>
```

**2. Reserve space for ads/embeds**
```html
<!-- ❌ No space reserved -->
<div id="ad"></div>

<!-- ✅ Reserve space with min-height -->
<div id="ad" style="min-height: 250px;">
  <!-- Ad loads here -->
</div>

<!-- ✅ Or explicit dimensions -->
<div id="ad" style="width: 300px; height: 250px;">
  <!-- Ad loads here -->
</div>
```

**3. Avoid inserting content above existing content**
```javascript
// ❌ Inserting above pushes content down
header.insertAdjacentHTML('afterend', '<div class="banner">...</div>');

// ✅ Insert at end or use fixed/sticky positioning
document.body.insertAdjacentHTML('beforeend', '<div class="banner">...</div>');

// ✅ Or position absolutely/fixed (doesn't affect layout)
<div class="banner" style="position: fixed; top: 0; left: 0; right: 0;">
  ...
</div>
```

**4. Optimize web font loading**
```css
/* ❌ FOUT (Flash of Unstyled Text) causes shift */
@font-face {
  font-family: 'Custom';
  src: url('custom.woff2');
}

/* ✅ Use font-display: optional (prevents shift) */
@font-face {
  font-family: 'Custom';
  src: url('custom.woff2');
  font-display: optional; /* No shift, uses fallback if not loaded quickly */
}

/* ✅ Or font-display: swap with size-adjust */
@font-face {
  font-family: 'Custom';
  src: url('custom.woff2');
  font-display: swap;
  size-adjust: 100%; /* Match fallback font size */
}
```

**5. Preload fonts to load earlier**
```html
<link
  rel="preload"
  href="/fonts/custom-font.woff2"
  as="font"
  type="font/woff2"
  crossorigin
>
```

**6. Use CSS transforms for animations**
```css
/* ❌ Animating position properties causes layout shifts */
.box {
  animation: moveDown 1s;
}

@keyframes moveDown {
  from { top: 0; }
  to { top: 100px; }
}

/* ✅ Use transform (doesn't affect layout) */
.box {
  animation: moveDown 1s;
}

@keyframes moveDown {
  from { transform: translateY(0); }
  to { transform: translateY(100px); }
}
```

**7. Reserve space for dynamic content**
```html
<!-- ❌ Content appears and shifts layout -->
<div id="dynamic-content"></div>

<!-- ✅ Skeleton/placeholder reserves space -->
<div id="dynamic-content" class="skeleton" style="min-height: 200px;">
  <!-- Loading skeleton shown until content loads -->
</div>

<style>
  .skeleton {
    background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
    background-size: 200% 100%;
    animation: loading 1.5s infinite;
  }

  @keyframes loading {
    0% { background-position: 200% 0; }
    100% { background-position: -200% 0; }
  }
</style>
```

#### CLS Common Issues & Fixes

**Issue: Images without dimensions**
- **Fix:** Add width/height attributes or aspect-ratio CSS
- **Tool:** Lighthouse, Chrome DevTools Layout Shift regions

**Issue: Web fonts causing FOUT/FOIT**
- **Fix:** Use font-display: optional or swap, preload fonts
- **Tool:** Chrome DevTools Network tab

**Issue: Ads/third-party embeds**
- **Fix:** Reserve space with min-height
- **Tool:** Lighthouse

**Issue: Dynamic content injection**
- **Fix:** Reserve space with skeleton placeholders
- **Tool:** Chrome DevTools Layout Shift regions

## Image Optimization

Images are typically 50-70% of total page weight. Optimization is critical.

### Format Selection

**Modern formats (best):**
- **WebP** - 25-35% smaller than JPG, supports transparency
- **AVIF** - 50% smaller than JPG, but slower to encode and limited browser support

**Legacy formats:**
- **JPG** - Photos, complex images
- **PNG** - Transparency needed, simple graphics
- **SVG** - Logos, icons, simple illustrations

**Format decision tree:**
1. Logo/icon/illustration? → **SVG**
2. Photo/complex image? → **WebP** with JPG fallback
3. Transparency needed? → **PNG** or **WebP**
4. Animated? → **GIF** (or video for better compression)

**Using modern formats with fallback:**
```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Description" width="800" height="600">
</picture>
```

### Compression

**Tools:**
- **Squoosh** - https://squoosh.app (online, visual comparison)
- **ImageOptim** - Mac app (lossless/lossy compression)
- **TinyPNG** - https://tinypng.com (online, lossy PNG/JPG)
- **Sharp** - Node.js library (automated compression)

**Compression targets:**
- **Hero images:** 100-200 KB
- **Content images:** 50-100 KB
- **Thumbnails:** 10-30 KB
- **Icons (PNG):** 5-10 KB (or use SVG)

**Quality settings:**
- **JPG:** 75-85 quality (sweet spot)
- **WebP:** 75-80 quality
- **PNG:** Optimize with tools (lossless compression)

### Responsive Images

**Using srcset for different screen sizes:**
```html
<img
  src="image-800w.jpg"
  srcset="
    image-400w.jpg 400w,
    image-800w.jpg 800w,
    image-1200w.jpg 1200w,
    image-1600w.jpg 1600w
  "
  sizes="(max-width: 640px) 100vw, (max-width: 1024px) 50vw, 800px"
  alt="Description"
  width="800"
  height="600"
  loading="lazy"
>
```

**How it works:**
- **srcset** - Available image sizes (width descriptor)
- **sizes** - How wide the image will be at different viewports
- Browser selects the best image based on device DPR and viewport

**Art direction (different crops for different screens):**
```html
<picture>
  <source
    media="(max-width: 640px)"
    srcset="hero-mobile.jpg"
  >
  <source
    media="(max-width: 1024px)"
    srcset="hero-tablet.jpg"
  >
  <img
    src="hero-desktop.jpg"
    alt="Hero image"
    width="1200"
    height="600"
  >
</picture>
```

### Lazy Loading

**Native lazy loading (simple, effective):**
```html
<!-- ✅ Lazy load below-the-fold images -->
<img src="image.jpg" alt="Description" loading="lazy" width="800" height="600">

<!-- ✅ Above-the-fold images load immediately -->
<img src="hero.jpg" alt="Hero" fetchpriority="high" width="1200" height="600">
```

**When to lazy load:**
- ✅ Below-the-fold images
- ✅ Image galleries
- ✅ Long pages with many images
- ❌ Hero images (above-the-fold)
- ❌ LCP images

**Browser support:** 97% (native `loading="lazy"`)

### Cloudflare Image Optimization

**Cloudflare Polish (automatic image optimization):**
1. Log into Cloudflare dashboard
2. Select domain
3. Speed → Optimization
4. Enable "Polish" (Lossy or Lossless)
5. Enable "WebP"

**What it does:**
- Automatically converts to WebP for supporting browsers
- Compresses images
- Serves from CDN edge

**Cost:** Included with Cloudflare Pro plan ($20/mo), or free with Cloudflare Images ($5/100k requests)

**Cloudflare Images (image resizing API):**
```html
<!-- Resize on-the-fly -->
<img src="https://imagedelivery.net/[ACCOUNT_HASH]/[IMAGE_ID]/w=800,h=600,fit=cover">

<!-- Multiple variants -->
<img
  srcset="
    https://imagedelivery.net/.../w=400 400w,
    https://imagedelivery.net/.../w=800 800w,
    https://imagedelivery.net/.../w=1200 1200w
  "
  sizes="(max-width: 640px) 100vw, 800px"
>
```

## JavaScript Optimization

JavaScript is the #1 performance bottleneck for most websites.

### Bundle Size Reduction

**Analyze bundle size:**
```bash
# Astro build analysis
npm run build
# Check dist/ folder sizes

# Or use bundle analyzer
npx vite-bundle-visualizer
```

**Reduction techniques:**
1. **Remove unused dependencies**
   ```bash
   npm uninstall unused-package
   ```

2. **Use lighter alternatives**
   ```javascript
   // ❌ Heavy library (70 KB)
   import moment from 'moment';

   // ✅ Lighter alternative (2 KB)
   import { format } from 'date-fns';
   ```

3. **Import only what you need**
   ```javascript
   // ❌ Imports entire library
   import _ from 'lodash';

   // ✅ Import specific function
   import debounce from 'lodash-es/debounce';
   ```

**Target:** Total JavaScript < 200 KB (compressed)

### Code Splitting

**Dynamic imports (load on demand):**
```javascript
// ❌ Load heavy library upfront
import Chart from 'chart.js';

// ✅ Load only when needed
button.addEventListener('click', async () => {
  const { default: Chart } = await import('chart.js');
  new Chart(ctx, config);
});
```

**Astro component-level code splitting:**
```astro
---
// Heavy component only loads if condition is true
const showChart = Astro.url.searchParams.has('chart');
---

{showChart && (
  <Chart client:visible />
)}
```

### Tree Shaking

Remove unused code from bundles.

**How to enable (Astro/Vite does this automatically):**
- Use ES modules (`import`/`export`)
- Avoid CommonJS (`require`)
- Avoid side effects in modules

**Check what's included:**
```bash
# Build and check sizes
npm run build

# Analyze bundle
npx vite-bundle-visualizer
```

### Minification

**Astro automatically minifies in production:**
```bash
npm run build  # Minifies JS, CSS, HTML
```

**What minification does:**
- Removes whitespace
- Shortens variable names
- Removes comments
- Optimizes syntax

**Before (10 KB):**
```javascript
function calculateTotalPrice(items) {
  let totalPrice = 0;
  for (let i = 0; i < items.length; i++) {
    totalPrice += items[i].price;
  }
  return totalPrice;
}
```

**After (0.5 KB):**
```javascript
function c(i){let t=0;for(let e=0;e<i.length;e++)t+=i[e].price;return t}
```

### Defer/Async Loading Strategies

**Script loading options:**

**1. Default (blocking):**
```html
<script src="app.js"></script>
<!-- Blocks HTML parsing until script downloads and executes -->
```

**2. Async (non-blocking download):**
```html
<script src="analytics.js" async></script>
<!-- Downloads in parallel, executes as soon as ready -->
<!-- Use for: Analytics, ads, independent scripts -->
```

**3. Defer (non-blocking, ordered execution):**
```html
<script src="app.js" defer></script>
<!-- Downloads in parallel, executes after HTML parsing -->
<!-- Use for: Main app scripts that depend on DOM -->
```

**Visual comparison:**
```
Blocking:  |--- HTML ---|--- Download + Execute ---|--- HTML ---|
Async:     |--- HTML + Download ---|X Execute X|--- HTML ---|
Defer:     |--- HTML + Download ---|--- HTML ---|X Execute X|
```

**Best practice:**
- **Async** - Analytics, ads, independent widgets
- **Defer** - Main app scripts, anything that needs DOM
- **Blocking** - Critical inline scripts only

## CSS Optimization

### Tailwind PurgeCSS Configuration

**Astro + Tailwind automatically purges unused CSS:**

```javascript
// tailwind.config.cjs
module.exports = {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

**What it does:**
- Scans content files for class names
- Removes unused Tailwind classes
- Reduces CSS from ~3 MB to ~10-50 KB

**Manual purge configuration:**
```javascript
// vite.config.js (if not using Tailwind)
import { defineConfig } from 'vite';
import purgecss from '@fullhuman/postcss-purgecss';

export default defineConfig({
  css: {
    postcss: {
      plugins: [
        purgecss({
          content: ['./src/**/*.{astro,html,js}'],
          safelist: ['class-to-keep', /^dynamic-/],
        }),
      ],
    },
  },
});
```

### Critical CSS Extraction

**Inline critical CSS, defer non-critical:**

```astro
---
// src/layouts/Layout.astro
---

<!DOCTYPE html>
<html>
<head>
  <!-- Critical CSS inlined -->
  <style>
    /* Above-the-fold styles */
    .hero { ... }
    .nav { ... }
    .button { ... }
  </style>

  <!-- Non-critical CSS deferred -->
  <link rel="preload" href="/styles/non-critical.css" as="style" onload="this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="/styles/non-critical.css"></noscript>
</head>
<body>
  <slot />
</body>
</html>
```

**Tools:**
- **Critical** - https://github.com/addyosmani/critical (extracts critical CSS)
- **Critters** - https://github.com/GoogleChromeLabs/critters (Astro plugin)

### Minification

**Astro automatically minifies CSS in production:**
```bash
npm run build  # Minifies CSS
```

**Manual minification (if needed):**
```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  build: {
    cssMinify: 'lightningcss', // Faster than default
  },
});
```

### Remove Unused Styles

**Use Chrome DevTools Coverage tool:**
1. Open DevTools (F12)
2. Cmd+Shift+P (Mac) or Ctrl+Shift+P (Windows)
3. Type "Coverage" → Show Coverage
4. Click Reload icon
5. View CSS coverage report

**Interpret results:**
- Red bars = unused CSS
- Green bars = used CSS
- Goal: 80%+ coverage (green)

**Common sources of unused CSS:**
- Unused Bootstrap/Foundation components
- Old legacy styles
- Commented-out but not deleted styles
- Framework CSS for unused features

## Astro-Specific Performance

### Static Generation Benefits

**Astro pre-renders HTML at build time (SSG):**

**Performance benefits:**
- ✅ No server processing time
- ✅ Instant TTFB from CDN
- ✅ Perfect for caching
- ✅ Extremely fast LCP
- ✅ No database queries at request time
- ✅ No server failures

**vs. Server-Side Rendering (SSR):**
```
SSG (Astro default):
Request → CDN (instant) → HTML
TTFB: 10-50ms ✅

SSR (traditional):
Request → Server → Database → Render → HTML
TTFB: 200-1000ms ❌
```

**When to use SSG (Astro default):**
- Marketing sites
- Business websites
- Blogs
- Documentation
- Landing pages
- Most content sites

**When you need SSR:**
- User-specific content (dashboards)
- Real-time data
- Dynamic based on request headers
- Server-side authentication

### Island Architecture (Partial Hydration)

**Astro's island architecture = Zero JS by default + selective hydration**

**How it works:**
```astro
---
// src/pages/index.astro
import StaticHeader from '@components/StaticHeader.astro';
import InteractiveCounter from '@components/InteractiveCounter.jsx';
import StaticFooter from '@components/StaticFooter.astro';
---

<!-- ✅ Static HTML (no JS) -->
<StaticHeader />

<!-- ✅ Interactive "island" (JS only for this) -->
<InteractiveCounter client:visible />

<!-- ✅ Static HTML (no JS) -->
<StaticFooter />
```

**Client directives:**
- `client:load` - Load JS immediately
- `client:idle` - Load when browser is idle
- `client:visible` - Load when element enters viewport (best for below-fold)
- `client:media` - Load when media query matches
- `client:only` - Skip SSR, client-side only

**Performance benefit:**
```
Traditional React site:
- HTML: 50 KB
- JavaScript: 500 KB
- Total: 550 KB

Astro with islands:
- HTML: 50 KB
- JavaScript: 20 KB (only interactive parts)
- Total: 70 KB ✅
```

### Component-Level Client-Side JS

**Only add JS to components that need it:**

```astro
---
// src/components/ContactForm.astro
// No client directive = no JS shipped
---

<form method="POST" action="/api/contact">
  <!-- Pure HTML form, works without JS -->
  <input type="text" name="name" required>
  <input type="email" name="email" required>
  <button type="submit">Send</button>
</form>
```

```jsx
// src/components/SearchWidget.jsx
// Has client directive = ships JS
export default function SearchWidget() {
  const [query, setQuery] = useState('');
  // Interactive search with React
  return <input value={query} onChange={e => setQuery(e.target.value)} />;
}
```

```astro
---
// src/pages/index.astro
import ContactForm from '@components/ContactForm.astro';
import SearchWidget from '@components/SearchWidget.jsx';
---

<!-- No JS -->
<ContactForm />

<!-- Ships React + component JS (only when visible) -->
<SearchWidget client:visible />
```

### Zero-JS by Default

**Astro ships zero JavaScript by default:**

```astro
---
// This page ships ZERO JavaScript
---

<html>
<head>
  <title>My Page</title>
</head>
<body>
  <header>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>

  <main>
    <h1>Welcome</h1>
    <p>Pure HTML, no JS needed.</p>
  </main>
</body>
</html>
```

**Result:**
- LCP: < 1 second ✅
- INP: N/A (no interactions) ✅
- CLS: 0 ✅
- Bundle size: 0 KB ✅
- Lighthouse score: 100 ✅

**Add JS only when needed:**
```astro
<!-- Add small inline script if needed -->
<script>
  // Runs once on page load
  document.querySelector('.mobile-menu-toggle').addEventListener('click', () => {
    document.querySelector('.mobile-menu').classList.toggle('open');
  });
</script>

<!-- Or import external script -->
<script src="/scripts/analytics.js" defer></script>
```

## Caching Strategies

### Browser Caching (Cache-Control Headers)

**Configure in Cloudflare Pages (`_headers` file):**

```
# public/_headers

/*
  Cache-Control: public, max-age=0, must-revalidate

/*.css
  Cache-Control: public, max-age=31536000, immutable

/*.js
  Cache-Control: public, max-age=31536000, immutable

/*.woff2
  Cache-Control: public, max-age=31536000, immutable

/*.jpg
  Cache-Control: public, max-age=31536000, immutable

/*.png
  Cache-Control: public, max-age=31536000, immutable

/*.webp
  Cache-Control: public, max-age=31536000, immutable

/*.svg
  Cache-Control: public, max-age=31536000, immutable
```

**What these headers mean:**
- `public` - Can be cached by CDN and browser
- `max-age=31536000` - Cache for 1 year (in seconds)
- `immutable` - Don't revalidate even on reload
- `max-age=0, must-revalidate` - Always revalidate (for HTML)

**Astro's built-in asset hashing:**
```html
<!-- Build generates unique filenames -->
<link rel="stylesheet" href="/assets/styles.a3f2b8.css">
<script src="/assets/app.7c8d4e.js"></script>

<!-- Can cache forever because filename changes when content changes -->
```

### Cloudflare Edge Caching

**Cloudflare caches at edge locations worldwide:**

**Default caching (automatic):**
- Static files (CSS, JS, images) cached automatically
- HTML cached based on headers

**Customize caching (Page Rules):**
1. Log into Cloudflare
2. Select domain
3. Rules → Page Rules → Create Page Rule
4. Pattern: `www.smithplumbing.com/*`
5. Settings:
   - Cache Level: Standard
   - Browser Cache TTL: 4 hours
   - Edge Cache TTL: 2 hours
6. Save

**Cache everything (including HTML):**
1. Create Page Rule
2. Pattern: `www.smithplumbing.com/*`
3. Setting: Cache Level → Cache Everything
4. Edge Cache TTL: 2 hours

**Purge cache when deploying:**
```bash
# Cloudflare Pages automatically purges cache on deploy
# Or manual purge via API/dashboard
```

### Service Workers

**Advanced: Offline support and custom caching**

```javascript
// public/sw.js
const CACHE_NAME = 'v1';
const urlsToCache = [
  '/',
  '/styles/main.css',
  '/scripts/app.js',
  '/images/logo.svg',
];

// Install service worker and cache files
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME).then((cache) => {
      return cache.addAll(urlsToCache);
    })
  );
});

// Serve from cache, fallback to network
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
```

**Register service worker:**
```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
  }
</script>
```

**Benefits:**
- Offline support
- Faster repeat visits
- Custom caching strategies

**Use cases:**
- PWAs (Progressive Web Apps)
- Offline documentation
- News sites (cache articles)

### Cache TTL Configuration

**TTL (Time To Live) recommendations:**

| Resource Type | Browser Cache | CDN Cache |
|--------------|---------------|-----------|
| HTML | 0 (revalidate) | 1-2 hours |
| CSS/JS (hashed) | 1 year | 1 year |
| Images (hashed) | 1 year | 1 year |
| Images (not hashed) | 1 day | 1 week |
| Fonts | 1 year | 1 year |
| API responses | 0 (no cache) | 5-60 minutes |

**Stale-while-revalidate pattern:**
```
Cache-Control: max-age=3600, stale-while-revalidate=86400
```
- Serves cached version for 1 hour
- After 1 hour, serves stale cache while fetching new version in background
- Updates cache for next request

## Font Optimization

### Font Subsetting

**Remove unused characters to reduce file size:**

```bash
# Install pyftsubset
pip install fonttools

# Subset to Latin characters only
pyftsubset font.ttf \
  --output-file=font-subset.woff2 \
  --flavor=woff2 \
  --unicodes=U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD
```

**Or use online tools:**
- **Font Squirrel Webfont Generator** - https://www.fontsquirrel.com/tools/webfont-generator
- **Fontie** - https://fontie.pixelsvsbytes.com/webfont-generator

**Size reduction:**
- Full font: 200-400 KB
- Latin subset: 20-40 KB ✅

### font-display Strategies

**Control how fonts load:**

```css
@font-face {
  font-family: 'Custom Font';
  src: url('/fonts/custom.woff2') format('woff2');
  font-display: swap; /* or optional, fallback, block */
  font-weight: 400;
  font-style: normal;
}
```

**font-display options:**

**1. `swap` (recommended for most cases)**
- Shows fallback font immediately
- Swaps to custom font when loaded
- May cause layout shift (CLS) if fonts are different sizes
```css
font-display: swap;
```

**2. `optional` (best for performance)**
- Shows fallback font immediately
- Only swaps if font loads within ~100ms
- No layout shift if font doesn't load quickly
- Best for avoiding CLS
```css
font-display: optional;
```

**3. `fallback`**
- Brief invisible period (~100ms)
- Shows fallback if custom font not loaded
- Swaps if loads within ~3 seconds
```css
font-display: fallback;
```

**4. `block`**
- Invisible text while font loads (up to 3 seconds)
- Shows custom font or fallback after timeout
- Not recommended (bad UX)
```css
font-display: block;
```

**Recommendation:**
- **Body text:** `font-display: optional` (avoid CLS)
- **Headings/brand:** `font-display: swap` (important to show custom font)

### WOFF2 Format

**Use WOFF2 (best compression):**

```css
@font-face {
  font-family: 'Custom Font';
  src: url('/fonts/custom.woff2') format('woff2'),
       url('/fonts/custom.woff') format('woff'); /* Fallback for old browsers */
  font-display: optional;
}
```

**Format comparison:**
- **TTF:** 200 KB (uncompressed)
- **WOFF:** 100 KB (compressed)
- **WOFF2:** 50 KB (better compression) ✅

**Browser support:** 97% (WOFF2)

### Preloading Fonts

**Preload critical fonts:**

```html
<link
  rel="preload"
  href="/fonts/custom-regular.woff2"
  as="font"
  type="font/woff2"
  crossorigin
>
```

**When to preload:**
- ✅ Fonts used above-the-fold
- ✅ Brand/heading fonts
- ❌ Body text fonts (if using font-display: optional)
- ❌ All font weights (only preload what's needed)

**Maximum preloads:** 1-2 fonts (preloading too many hurts performance)

### System Font Fallbacks

**Use system fonts as fallbacks (no download needed):**

```css
body {
  font-family:
    'Custom Font',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
}
```

**Or use system fonts only (zero font load time):**
```css
body {
  font-family:
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
}
```

**System font stack benefits:**
- ✅ Zero load time
- ✅ Zero CLS
- ✅ Familiar to users (native to OS)
- ✅ Great performance

**Consider system fonts for:**
- Body text (performance priority)
- Dashboards/apps (functionality over brand)
- MVPs (ship faster)

## Third-Party Scripts

### Lazy Loading Strategies

**Load on user interaction:**
```html
<!-- Load chat widget only when user clicks -->
<button id="open-chat">Chat with us</button>

<script>
  document.getElementById('open-chat').addEventListener('click', () => {
    const script = document.createElement('script');
    script.src = 'https://example.com/chat-widget.js';
    document.head.appendChild(script);
  }, { once: true });
</script>
```

**Load when scrolling to element:**
```javascript
// Intersection Observer
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const script = document.createElement('script');
      script.src = 'https://example.com/widget.js';
      document.head.appendChild(script);
      observer.unobserve(entry.target);
    }
  });
});

observer.observe(document.getElementById('widget-container'));
```

**Astro client:visible approach:**
```astro
---
import ChatWidget from '@components/ChatWidget.jsx';
---

<!-- Only loads JS when scrolled into view -->
<ChatWidget client:visible />
```

### Self-Hosting When Possible

**Instead of third-party CDN:**
```html
<!-- ❌ Third-party CDN (DNS lookup, SSL handshake overhead) -->
<script src="https://cdn.example.com/library.js"></script>

<!-- ✅ Self-hosted (same origin, already connected) -->
<script src="/scripts/library.js"></script>
```

**Benefits:**
- No extra DNS lookup
- No extra SSL handshake
- Better caching control
- No SPOF (single point of failure)
- Privacy (no third-party tracking)

**Self-host these:**
- Google Fonts (use Fontsource)
- Google Analytics (use Plausible or self-hosted)
- jQuery, Bootstrap, etc.

**Fontsource example:**
```bash
npm install @fontsource/inter

# In Astro component
import '@fontsource/inter';
import '@fontsource/inter/600.css';
```

### Façade Pattern for Embeds

**Replace heavy embeds with lightweight previews:**

**YouTube embed (traditional):**
```html
<!-- ❌ Loads 1 MB+ of YouTube scripts -->
<iframe
  src="https://www.youtube.com/embed/VIDEO_ID"
  width="560"
  height="315"
></iframe>
```

**YouTube façade (optimized):**
```html
<!-- ✅ Lightweight preview, loads iframe on click -->
<div class="youtube-facade" data-video-id="VIDEO_ID">
  <img
    src="https://img.youtube.com/vi/VIDEO_ID/maxresdefault.jpg"
    alt="Video thumbnail"
  >
  <button class="play-button">Play</button>
</div>

<style>
  .youtube-facade {
    position: relative;
    cursor: pointer;
  }
  .play-button {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    /* Style as YouTube play button */
  }
</style>

<script>
  document.querySelectorAll('.youtube-facade').forEach(facade => {
    facade.addEventListener('click', () => {
      const videoId = facade.dataset.videoId;
      const iframe = document.createElement('iframe');
      iframe.src = `https://www.youtube.com/embed/${videoId}?autoplay=1`;
      iframe.width = '560';
      iframe.height = '315';
      iframe.allow = 'autoplay';
      facade.replaceWith(iframe);
    });
  });
</script>
```

**Libraries:**
- **lite-youtube-embed** - https://github.com/paulirish/lite-youtube-embed
- **React Lite YouTube Embed** - https://github.com/ibrahimcesar/react-lite-youtube-embed

**Savings:**
- Traditional embed: 1.2 MB
- Façade: 200 KB (image) + 0 KB JS until click
- **Savings: 1 MB+** ✅

## Testing and Monitoring

### Google PageSpeed Insights

**URL:** https://pagespeed.web.dev

**How to use:**
1. Enter your URL
2. Click "Analyze"
3. View mobile and desktop scores
4. Review Core Web Vitals
5. Check opportunities and diagnostics

**Target scores:**
- **Performance:** 90+ (desktop), 80+ (mobile)
- **Accessibility:** 95+
- **Best Practices:** 95+
- **SEO:** 95+

**Focus on:**
- Core Web Vitals (LCP, INP, CLS)
- Opportunities (biggest wins)
- Diagnostics (issues)

### Lighthouse CI Integration

**Run Lighthouse in CI/CD pipeline:**

```bash
# Install
npm install -g @lhci/cli

# Configure
# lighthouserc.js
module.exports = {
  ci: {
    collect: {
      url: ['http://localhost:3000'],
      numberOfRuns: 3,
    },
    assert: {
      preset: 'lighthouse:recommended',
      assertions: {
        'categories:performance': ['error', { minScore: 0.9 }],
        'categories:accessibility': ['error', { minScore: 0.95 }],
        'first-contentful-paint': ['error', { maxNumericValue: 2000 }],
        'largest-contentful-paint': ['error', { maxNumericValue: 2500 }],
        'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }],
      },
    },
    upload: {
      target: 'temporary-public-storage',
    },
  },
};

# Run
lhci autorun
```

**GitHub Actions example:**
```yaml
name: Lighthouse CI
on: [push]
jobs:
  lighthouse:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npm run build
      - run: npm install -g @lhci/cli
      - run: lhci autorun
```

### WebPageTest

**URL:** https://www.webpagetest.org

**Features:**
- Test from multiple locations
- Test on real devices
- Filmstrip view (visual loading)
- Waterfall chart (network requests)
- Repeat view (cached performance)

**How to use:**
1. Enter URL
2. Select location (closest to target audience)
3. Select browser/device
4. Click "Start Test"
5. Wait for results (2-5 minutes)

**Key metrics:**
- TTFB (Time to First Byte)
- Start Render
- LCP
- Total Load Time
- Fully Loaded Time

**Advanced:**
- Test with slow connections (3G, 4G)
- Compare before/after optimizations
- Test authenticated pages
- Custom scripts

### Chrome DevTools Performance Tab

**How to profile:**
1. Open DevTools (F12)
2. Click "Performance" tab
3. Click Record button (●)
4. Interact with page
5. Click Stop
6. Analyze timeline

**What to look for:**
- **Long tasks** (> 50ms) - Red corners on tasks
- **Layout shifts** - Blue bars with "Layout Shift" label
- **Main thread activity** - JavaScript execution time
- **Network requests** - Blocking requests
- **Rendering** - Paint and composite time

**Identify INP issues:**
1. Click "Interactions" in summary
2. Find slow interactions (> 200ms)
3. Click interaction to see breakdown
4. Optimize identified bottlenecks

### Real User Monitoring (RUM)

**Monitor actual user experiences:**

**Tools:**
- **Google Analytics 4** - Basic Core Web Vitals
- **Cloudflare Web Analytics** - Free, privacy-focused
- **SpeedCurve** - Detailed RUM and synthetic monitoring
- **web-vitals library** - Send to your own analytics

**web-vitals example:**
```bash
npm install web-vitals
```

```javascript
// public/vitals.js
import { onCLS, onFID, onLCP, onINP } from 'web-vitals';

function sendToAnalytics({ name, value, id }) {
  // Send to your analytics endpoint
  fetch('/api/vitals', {
    method: 'POST',
    body: JSON.stringify({ name, value, id }),
    headers: { 'Content-Type': 'application/json' },
  });
}

onCLS(sendToAnalytics);
onFID(sendToAnalytics);
onLCP(sendToAnalytics);
onINP(sendToAnalytics);
```

**Why RUM matters:**
- Lab tests don't reflect real-world conditions
- RUM captures actual user experiences
- Different devices, connections, locations
- Identifies issues that only affect some users

## Performance Budget

**Set targets and enforce them:**

### Setting Targets

**Example performance budget:**

| Metric | Target | Max |
|--------|--------|-----|
| LCP | < 2.0s | 2.5s |
| INP | < 150ms | 200ms |
| CLS | < 0.05 | 0.1 |
| Total JS | < 150 KB | 200 KB |
| Total CSS | < 50 KB | 75 KB |
| Total Images | < 500 KB | 1 MB |
| Total Page Size | < 1 MB | 1.5 MB |
| Requests | < 30 | 50 |

### Automated Enforcement in CI/CD

**Lighthouse CI assertions:**
```javascript
// lighthouserc.js
module.exports = {
  ci: {
    assert: {
      assertions: {
        'largest-contentful-paint': ['error', { maxNumericValue: 2500 }],
        'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }],
        'total-byte-weight': ['error', { maxNumericValue: 1500000 }], // 1.5 MB
        'resource-summary:script:size': ['error', { maxNumericValue: 200000 }], // 200 KB JS
      },
    },
  },
};
```

**Bundle size limits (webpack/vite):**
```javascript
// vite.config.js
export default {
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          if (id.includes('node_modules')) {
            return 'vendor';
          }
        },
      },
    },
    chunkSizeWarningLimit: 500, // Warn if chunk > 500 KB
  },
};
```

### Tracking Over Time

**Monitor trends:**
1. Set up RUM (Real User Monitoring)
2. Track weekly/monthly averages
3. Alert on regressions
4. Review before major releases

**Tools:**
- **Cloudflare Web Analytics** - Free dashboard
- **Google Search Console** - Core Web Vitals report
- **SpeedCurve** - Historical performance tracking

## Cloudflare-Specific Features

Cloudflare provides automatic performance optimizations.

### Auto Minify

**Automatically minifies CSS, JS, HTML:**

1. Log into Cloudflare dashboard
2. Select domain
3. Speed → Optimization
4. Enable Auto Minify:
   - ✅ JavaScript
   - ✅ CSS
   - ✅ HTML

**What it does:**
- Removes whitespace
- Removes comments
- Shortens variable names (JS only if safe)

**Savings:** 20-40% reduction in file sizes

### Rocket Loader

**Asynchronously loads JavaScript:**

1. Speed → Optimization
2. Enable "Rocket Loader"

**What it does:**
- Defers JavaScript loading
- Loads scripts asynchronously
- Improves page load time

**Warning:** May break some scripts (test thoroughly)

**When to use:**
- Site has many blocking scripts
- Can't modify HTML to add defer/async
- After testing on staging

**When to avoid:**
- Modern site with async/defer already
- Interactive apps that need immediate JS

### Mirage

**Lazy loads images automatically:**

1. Speed → Optimization
2. Enable "Mirage"

**What it does:**
- Automatically lazy loads images
- Shows low-res placeholder
- Loads full image when scrolling

**Cost:** Requires Cloudflare Pro plan ($20/mo)

**Alternative:** Use native `loading="lazy"` (free, works everywhere)

### Polish

**Automatic image optimization:**

1. Speed → Optimization
2. Enable "Polish"
3. Select "Lossy" or "Lossless"
4. Enable "WebP"

**What it does:**
- Compresses images
- Converts to WebP for supporting browsers
- Serves optimized version from CDN

**Cost:** Requires Cloudflare Pro plan ($20/mo)

**Savings:**
- Lossy: 30-50% size reduction
- Lossless: 10-20% size reduction
- WebP: Additional 25-35% reduction

## Cross-References

**Related documentation:**
- [SEO Standards](./seo.md) - Performance affects SEO rankings (Core Web Vitals)
- [Accessibility Standards](./accessibility.md) - Performance and accessibility overlap
- [Testing & Debugging](../workflow/phase-3-testing-debugging.md) - Performance testing in your workflow
- [Cloudflare Pages](../hosting-tools/cloudflare-pages.md) - Hosting configuration for performance
- [Cloudflare CDN](../hosting-tools/cloudflare-cdn.md) - CDN configuration
- [Quality Standards Overview](./README.md) - Back to quality standards home

---

**Remember:** Performance is not a one-time task. Monitor continuously, test on real devices, and optimize iteratively. Prioritize Core Web Vitals (LCP, INP, CLS) as they directly impact SEO rankings and user experience.
