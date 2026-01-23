# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static website for Minnehaha United Methodist Church (Minneapolis, MN). Hosted at `https://www.minnehaha.org` (subdirectory deployment).

## Commands

```bash
hugo server          # Start dev server at localhost:1313
hugo server -D       # Dev server with drafts visible
hugo                 # Build site to public/
hugo --minify        # Production build with minification
```

## Architecture

### Content Flow
```
content/homepage/*.md  →  layouts/partials/homepage-card.html  →  layouts/index.html
```
Homepage uses Markdown files with YAML front matter for non-technical content editing.

### Key Files
| File | Purpose |
|------|---------|
| `hugo.toml` | Site config, menus, params |
| `layouts/_default/baseof.html` | Base template (CDN scripts, meta) |
| `layouts/partials/homepage-card.html` | Card component (image/video/text types) |
| `static/css/custom.css` | All CSS customizations |
| `static/layout/js/main.js` | Swiper init, legacy function stubs |

### CSS Strategy
- **Never modify** `static/layout/style.css` (original theme)
- **All changes** go in `static/css/custom.css`
- Uses CSS Grid for layouts (replaced Isotope.js)
- Uses CSS Custom Properties for theming
- Responsive breakpoints: 960px, 768px, 480px

### JavaScript
- jQuery 3.7.1 and Swiper.js 11 loaded from CDN with SRI hashes
- Legacy function stubs in main.js kept for compatibility

## Critical: Subdirectory Deployment

Production is hosted at `https://minnehaha.org` (subdirectory).

- `hugo.toml` uses `baseURL = '/'` for local development
- GitHub Actions workflow sets `--baseURL` for production builds
- **All paths in templates must use `| relURL`**:
```html
<img src="{{ "/images/photo.jpg" | relURL }}">
<a href="{{ "/" | relURL }}">Home</a>
```

## Common Gotchas

1. **Hugo caching**: Delete `public/` and restart server if changes don't appear
2. **SRI hash mismatch**: Browser blocks scripts with wrong integrity hashes
3. **Front matter**: Use YAML format (not TOML) in content files
4. **Image paths**: Start with `/images/` (not `images/` or `./images/`)
5. **jQuery timing**: Scripts in templates run before jQuery loads; use main.js for init

## Updating CDN Libraries

Generate new SRI hash:
```bash
curl -s [CDN_URL] | openssl dgst -sha256 -binary | openssl base64
```
Update both `src` and `integrity` attributes in baseof.html.

## Testing Checklist

- Site builds without errors (`hugo`)
- Cards render properly (image, video, text-only)
- Slider works with navigation
- Responsive layout at all breakpoints
- No JavaScript console errors
- Keyboard navigation works

## Additional Documentation

- `AGENTS.md` - Detailed contributor guidelines
- `docs/CONTENT-MANAGEMENT.md` - Content editor guide
