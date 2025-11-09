- markdown ---------------------------------------------------------------------

# Optimization Guide
*For Luxury Car Rental Website*

## 🚀 Critical Rendering Path

### 1. HTML Optimization
```html
<!-- Inline critical CSS -->
<style>
  /* Above-the-fold styles only */
  .header, .hero, .primary-cta { /* styles */ }
</style>

<!-- Defer non-critical CSS -->
<link rel="preload" href="non-critical.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="non-critical.css"></noscript>

<!-- Preload key resources -->
<link rel="preload" href="hero-image.webp" as="image">
<link rel="preload" href="critical-font.woff2" as="font" crossorigin>



- CSS Optimization Strategy------------------------------------------------------------

/* Use CSS variables for theming */
:root {
  --primary-color: #1a1a1a;
  --secondary-color: #d4af37;
  --font-main: 'Proxima Nova', sans-serif;
}

/* Critical CSS (inline in head) */
.hero, .navigation, .primary-content { /* styles */ }

/* Non-critical CSS (loaded async) */
.testimonials, .footer, .secondary-content { /* styles */ }


- JavaScript Loading Strategy --------------------------------------------------------

// Critical JS (inline in head)
const criticalFunctions = {
  initNavigation: function() { /* */ },
  setupSearch: function() { /* */ }
};

// Defer non-critical JS
<script defer src="/assets/js/vehicle-filter.js"></script>
<script defer src="/assets/js/booking-engine.js"></script>

// Lazy load heavy modules
if (isVehiclePage) {
  import('./modules/vehicle-comparison.js');
}



- Image Optimization ------------------------------------------------------------------

<picture>
  <source 
    media="(max-width: 768px)"
    srcset="
      vehicle-400.webp 400w,
      vehicle-800.webp 800w
    "
    sizes="100vw"
    type="image/webp">
  <source 
    srcset="
      vehicle-800.webp 800w,
      vehicle-1200.webp 1200w,
      vehicle-2000.webp 2000w
    "
    sizes="(max-width: 1200px) 100vw, 1200px"
    type="image/webp">
  <img 
    src="vehicle-800.jpg" 
    alt="Luxury Vehicle"
    loading="lazy"
    width="1200" 
    height="800">
</picture>

- --------------------------------------------------------------------------
# Performance Budget (`performance-budget.md`)

```markdown
# Performance Budget
*Last Updated: [Date]*

## Core Web Vitals Targets
- **LCP (Largest Contentful Paint):** < 2.5s
- **FID (First Input Delay):** < 100ms  
- **CLS (Cumulative Layout Shift):** < 0.1
- **TBT (Total Blocking Time):** < 200ms

## Loading Budget
| Resource Type | Budget per Page | Notes |
|---------------|-----------------|-------|
| HTML | ≤ 15KB | Gzipped |
| CSS | ≤ 20KB | Critical CSS ≤ 10KB |
| JavaScript | ≤ 50KB | Above-fold JS ≤ 15KB |
| Images | ≤ 200KB | Hero images ≤ 50KB |
| Fonts | ≤ 30KB | WOFF2 format only |
| Total Page Weight | ≤ 300KB | Without lazy-loaded content |

## Image Quality Standards
| Image Type | Max Width | Format | Quality |
|------------|-----------|--------|---------|
| Hero Images | 2000px | WebP + JPEG | 85% |
| Content Images | 1200px | WebP + JPEG | 80% |
| Thumbnails | 400px | WebP | 75% |
| Icons | 64px | SVG | Vector |

## JavaScript Budget
- Initial Bundle: ≤ 50KB
- Third-party Scripts: ≤ 30KB
- Time to Interactive: < 3s
- Main Thread Work: < 200ms

## Network Conditions
| Connection Type | Target Load Time |
|-----------------|------------------|
| 4G (Good) | < 3s |
| 3G (Slow) | < 5s |
| 2G (Very Slow) | < 8s |

## Monitoring & Alerts
- Weekly performance audits
- Alert if LCP > 3s
- Alert if TTI > 5s
- Alert if image weight > 250KB
```

# Optimization Guide (`optimization-guide.md`)

```markdown
# Optimization Guide
*For Luxury Car Rental Website*

## 🚀 Critical Rendering Path

### 1. HTML Optimization
```html
<!-- Inline critical CSS -->
<style>
  /* Above-the-fold styles only */
  .header, .hero, .primary-cta { /* styles */ }
</style>

<!-- Defer non-critical CSS -->
<link rel="preload" href="non-critical.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="non-critical.css"></noscript>

<!-- Preload key resources -->
<link rel="preload" href="hero-image.webp" as="image">
<link rel="preload" href="critical-font.woff2" as="font" crossorigin>
```

### 2. CSS Optimization Strategy
```css
/* Use CSS variables for theming */
:root {
  --primary-color: #1a1a1a;
  --secondary-color: #d4af37;
  --font-main: 'Proxima Nova', sans-serif;
}

/* Critical CSS (inline in head) */
.hero, .navigation, .primary-content { /* styles */ }

/* Non-critical CSS (loaded async) */
.testimonials, .footer, .secondary-content { /* styles */ }
```

### 3. JavaScript Loading Strategy
```javascript
// Critical JS (inline in head)
const criticalFunctions = {
  initNavigation: function() { /* */ },
  setupSearch: function() { /* */ }
};

// Defer non-critical JS
<script defer src="/assets/js/vehicle-filter.js"></script>
<script defer src="/assets/js/booking-engine.js"></script>

// Lazy load heavy modules
if (isVehiclePage) {
  import('./modules/vehicle-comparison.js');
}
```

## 🖼️ Image Optimization

### 1. Responsive Images
```html
<picture>
  <source 
    media="(max-width: 768px)"
    srcset="
      vehicle-400.webp 400w,
      vehicle-800.webp 800w
    "
    sizes="100vw"
    type="image/webp">
  <source 
    srcset="
      vehicle-800.webp 800w,
      vehicle-1200.webp 1200w,
      vehicle-2000.webp 2000w
    "
    sizes="(max-width: 1200px) 100vw, 1200px"
    type="image/webp">
  <img 
    src="vehicle-800.jpg" 
    alt="Luxury Vehicle"
    loading="lazy"
    width="1200" 
    height="800">
</picture>
```

### 2. Lazy Loading Strategy
```javascript
// Intersection Observer for images
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      img.classList.remove('lazy');
      imageObserver.unobserve(img);
    }
  });
});

document.querySelectorAll('img.lazy').forEach(img => {
  imageObserver.observe(img);
});
```

## 📦 Asset Delivery

### 1. Font Loading
```css
/* Font display strategy */
@font-face {
  font-family: 'Proxima Nova';
  src: url('/assets/fonts/proxima-nova.woff2') format('woff2');
  font-display: swap;
  font-weight: 400;
}

/* Critical font subset */
@font-face {
  font-family: 'Proxima Nova Subset';
  src: url('/assets/fonts/proxima-nova-subset.woff2') format('woff2');
  font-display: block;
  unicode-range: U+0020-007F;
}
```

### 2. Caching Strategy
```
# .htaccess or server config
# Cache static assets
<FilesMatch "\.(webp|jpg|jpeg|png|gif|svg|woff2)$">
  Header set Cache-Control "max-age=31536000, immutable"
</FilesMatch>

# Cache CSS and JS
<FilesMatch "\.(css|js)$">
  Header set Cache-Control "max-age=604800, public"
</FilesMatch>
```

## 🔧 Build Process Optimizations

### 1. CSS Processing
```javascript
// Build script example
const postcss = require('postcss')([
  require('autoprefixer'),
  require('cssnano')({
    preset: ['default', { discardComments: { removeAll: true } }]
  })
]);
```

### 2. JavaScript Bundling
```javascript
// Webpack config for code splitting
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all',
        },
        common: {
          name: 'common',
          minChunks: 2,
          chunks: 'all',
          enforce: true
        }
      }
    }
  }
};
```

## 📊 Monitoring & Testing

### 1. Performance Testing
```javascript
// Performance monitoring
const observer = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    if (entry.name === 'first-contentful-paint') {
      console.log('FCP:', entry.startTime);
    }
  }
});

observer.observe({entryTypes: ['paint', 'navigation']});
```

### 2. Bundle Analysis
```bash
# Analyze bundle size
npx webpack-bundle-analyzer dist/stats.json

# Check performance budget
npx bundlesize -f dist/*.js -s 50KB
```

## 🎯 Quick Wins
1. **Enable Gzip/Brotli compression**
2. **Implement CDN for static assets**
3. **Optimize hero images first**
4. **Remove unused CSS/JS**
5. **Implement service worker for caching**
```

# Loading Strategy (`loading-strategy.md`)

```markdown
# Loading Strategy
*Progressive Loading for Luxury Car Rental*

## 🎯 Loading Priorities

### Priority 1: Critical Resources (0-1s)
```
✓ HTML structure
✓ Critical CSS (inline)
✓ Critical JavaScript (inline)
✓ Hero image (preload)
✓ Web fonts (preload subset)
```

### Priority 2: Essential Content (1-3s)
```
✓ Navigation functionality
✓ Search functionality
✓ Primary vehicle images
✓ Booking form skeleton
✓ Core styling
```

### Priority 3: Secondary Content (3-5s)
```
✓ Vehicle galleries
✓ Testimonials
✓ Location maps
✓ Additional styling
✓ Analytics scripts
```

### Priority 4: Enhanced Features (>5s)
```
✓ Vehicle comparisons
✓ Image zoom features
✓ Background videos
✓ Social media integrations
```

## 🔄 Progressive Loading Phases

### Phase 1: Initial Render (0-100ms)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    /* Critical CSS - 8KB max */
    .header, .hero, .cta-button { /* styles */ }
  </style>
  <script>
    // Critical JS - 3KB max
    function setupCoreInteractions() { /* */ }
  </script>
</head>
<body>
  <!-- Skeleton screens -->
  <div class="skeleton-header"></div>
  <div class="skeleton-hero"></div>
</body>
</html>
```

### Phase 2: Content Hydration (100-1000ms)
```javascript
// Load essential content
Promise.all([
  loadFonts(),
  loadHeroImage(),
  setupNavigation(),
  initSearch()
]).then(() => {
  removeSkeletonScreens();
});
```

### Phase 3: Full Interaction (1000-3000ms)
```javascript
// Lazy load remaining content
const lazyModules = [
  import('./modules/vehicle-filter.js'),
  import('./modules/booking-form.js'),
  import('./modules/image-gallery.js')
];

Promise.all(lazyModules).then(() => {
  enableFullInteractivity();
});
```

## 🖼️ Image Loading Strategy

### 1. Hero Images
```html
<!-- Preload smallest hero image -->
<link rel="preload" as="image" href="hero-400.webp" imagesrcset="hero-400.webp 400w, hero-800.webp 800w" imagesizes="100vw">

<!-- Progressive loading -->
<img 
  src="hero-400.webp" 
  srcset="hero-400.webp 400w, hero-800.webp 800w, hero-1200.webp 1200w"
  sizes="(max-width: 768px) 100vw, 1200px"
  alt="Luxury Vehicle"
  loading="eager">
```

### 2. Content Images
```html
<!-- Lazy loading with placeholder -->
<img 
  data-src="vehicle-gallery-1.webp" 
  src="placeholder-20px.jpg"
  class="lazy-image"
  alt="Vehicle Interior"
  loading="lazy"
  width="800" 
  height="600">
```

### 3. Background Images
```css
.vehicle-card {
  background-image: url('placeholder-20px.jpg');
}

.vehicle-card.loaded {
  background-image: url('vehicle-image-800.webp');
}
```

## 📚 Font Loading Strategy

### 1. Font Subsetting
```bash
# Create Latin subset only
pyftsubset font.woff2 --output-file=font-latin.woff2 --unicodes="U+0020-007F"
```

### 2. Font Loading
```css
/* Critical font for headings */
@font-face {
  font-family: 'Gilroy Subset';
  src: url('/assets/fonts/gilroy-subset.woff2') format('woff2');
  font-display: block;
  unicode-range: U+0041-005A, U+0061-007A;
}

/* Full font for body */
@font-face {
  font-family: 'Proxima Nova';
  src: url('/assets/fonts/proxima-nova.woff2') format('woff2');
  font-display: swap;
}
```

## 🔄 JavaScript Loading Strategy

### 1. Critical Scripts (Inline)
```html
<script>
// 2KB max - core functionality only
window.APP = {
  init: function() {
    this.setupNavigation();
    this.handleSearch();
  },
  setupNavigation: function() { /* */ },
  handleSearch: function() { /* */ }
};
</script>
```

### 2. Essential Scripts (Deferred)
```html
<script defer src="/assets/js/vehicle-listing.js"></script>
<script defer src="/assets/js/booking-engine.js"></script>
```

### 3. Secondary Scripts (Lazy Load)
```javascript
// Load when needed
if (document.querySelector('.vehicle-comparison')) {
  import('./modules/vehicle-comparison.js');
}

// Load on user interaction
document.getElementById('view-gallery').addEventListener('click', () => {
  import('./modules/image-zoom.js');
});
```

## 🗂️ Code Splitting Strategy

### 1. Route-based Splitting
```javascript
// Homepage
const HomePage = () => import('./pages/Homepage.vue');

// Vehicle pages
const VehicleListing = () => import('./pages/VehicleListing.vue');
const VehicleDetails = () => import('./pages/VehicleDetails.vue');

// Booking flow
const BookingProcess = () => import('./pages/BookingProcess.vue');
```

### 2. Component-based Splitting
```javascript
// Heavy components
const ImageGallery = () => import('./components/ImageGallery.vue');
const VehicleComparison = () => import('./components/VehicleComparison.vue');
const InteractiveMap = () => import('./components/InteractiveMap.vue');
```

### 3. Function-based Splitting
```javascript
// Heavy utilities
const loadImageProcessor = () => import('./utils/image-processor.js');
const loadPaymentGateway = () => import('./utils/payment-gateway.js');
```

## 📱 Mobile-First Loading

### 1. Conditional Loading
```javascript
// Load mobile-optimized images
const isMobile = window.innerWidth < 768;
const imageSize = isMobile ? '400w' : '1200w';

// Load touch-optimized components
if ('ontouchstart' in window) {
  import('./components/touch-gallery.js');
} else {
  import('./components/desktop-gallery.js');
}
```

### 2. Network-Aware Loading
```javascript
// Check connection speed
const connection = navigator.connection;
if (connection) {
  if (connection.saveData) {
    loadLowQualityImages();
  } else if (connection.effectiveType === '4g') {
    loadHighQualityImages();
  }
}
```

## 🎪 Skeleton Screens Strategy

### 1. Content Placeholders
```html
<!-- Vehicle card skeleton -->
<div class="vehicle-card-skeleton">
  <div class="skeleton-image"></div>
  <div class="skeleton-text short"></div>
  <div class="skeleton-text long"></div>
  <div class="skeleton-button"></div>
</div>
```

### 2. Progressive Reveal
```javascript
// Reveal content as it loads
function revealContent(element) {
  element.style.opacity = '0';
  element.classList.remove('skeleton');
  
  requestAnimationFrame(() => {
    element.style.transition = 'opacity 0.3s ease';
    element.style.opacity = '1';
  });
}
```

## 📊 Performance Monitoring

### 1. Real User Monitoring
```javascript
// Track Core Web Vitals
import {getCLS, getFID, getLCP} from 'web-vitals';

getCLS(console.log);
getFID(console.log);
getLCP(console.log);
```

### 2. Custom Metrics
```javascript
// Track business metrics
const performanceMetrics = {
  timeToFirstVehicle: 0,
  timeToBookingForm: 0,
  imageLoadComplete: 0
};
```

This loading strategy ensures your luxury car rental website loads progressively, providing the best possible user experience while maintaining optimal performance.
```

These three documents provide a comprehensive performance framework that will keep your luxury car rental website loading quickly despite its sophisticated features and high-quality media content.

