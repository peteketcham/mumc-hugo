# Lighthouse Performance Fixes

This document tracks remaining performance and accessibility improvements identified from a Lighthouse audit (January 2026).

## Completed Fixes

- [x] **Meta viewport** - Removed `maximum-scale=1` to allow zooming (accessibility)
- [x] **Image dimensions** - Added width/height attributes to slider images (reduces CLS)
- [x] **Heading hierarchy** - Changed h3 elements to paragraphs on homepage (accessibility)

## Remaining Fixes (Medium Priority)

### Performance

| Issue | Est. Savings | Fix |
|-------|--------------|-----|
| Unused CSS (style.css) | ~195KB | Use PurgeCSS to remove unused rules, or manually audit |
| Unused CSS (animate.css) | ~47KB | Remove if animations not used, or load conditionally |
| Convert images to WebP | ~2MB | Use Hugo image processing or build script to generate WebP with JPG fallbacks |
| Cache headers | ~4MB | Configure server/CDN caching (Cache-Control headers) |
| Minify CSS/JS | ~62KB | Hugo `--minify` flag handles this in production builds |

### Accessibility

| Issue | Fix |
|-------|-----|
| Touch targets too small | Increase padding on mobile nav items to min 44x44px |
| Add image dimensions to card images | Update homepage-card.html partial to include width/height |

## Implementation Notes

### WebP Conversion

Hugo can process images with WebP output:
```html
{{ $img := resources.Get "images/photo.jpg" }}
{{ $webp := $img.Resize "600x webp" }}
<picture>
  <source srcset="{{ $webp.RelPermalink }}" type="image/webp">
  <img src="{{ $img.RelPermalink }}" alt="...">
</picture>
```

### PurgeCSS

Can be added to build pipeline:
```bash
npm install -g purgecss
purgecss --css public/**/*.css --content public/**/*.html --output public/
```

### Cache Headers

For GitHub Pages, caching is handled automatically. For custom hosting, add to server config:
```
# Apache .htaccess
<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
  ExpiresByType text/css "access plus 1 month"
  ExpiresByType application/javascript "access plus 1 month"
</IfModule>
```

## Lighthouse Scores (Before Fixes)

| Category | Score |
|----------|-------|
| Performance | 62% |
| Accessibility | 89% |
| Best Practices | 100% |
| SEO | 100% |

Re-run Lighthouse after implementing fixes to measure improvement.
