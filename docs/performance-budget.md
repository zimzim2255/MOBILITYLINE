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