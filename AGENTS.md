# Agents Guide

Guidelines for AI coding assistants and human contributors working on the Minnehaha UMC website.

## Project Overview

This is a Hugo static site for a church in Minneapolis. The site prioritizes:

1. **Ease of content management** for non-technical staff
2. **Accessibility** for all users
3. **Performance** on all devices and connections
4. **Maintainability** with clear code organization

## Architecture Decisions

### Content Structure

Homepage content uses Hugo's content management system:

```
content/homepage/*.md  →  Rendered by layouts/partials/homepage-card.html
                      →  Displayed on layouts/index.html
```

Each card is a standalone Markdown file with YAML front matter. This allows non-technical users to edit content without touching templates.

### CSS Strategy

**Do not modify** `static/layout/style.css` - this is the original theme file.

**All customizations** go in `static/css/custom.css`, which:
- Uses CSS Custom Properties for theming
- Provides CSS Grid layout (replacing Isotope.js)
- Includes Swiper.js slider styles
- Handles accessibility and responsive design

### JavaScript Strategy

- **jQuery 3.7.1** - Required for legacy theme compatibility
- **Swiper.js 11** - Modern slider (replaced Flexslider)
- **No Isotope** - Replaced with CSS Grid for layout

Legacy functions in `static/layout/js/main.js` are kept for compatibility but may be empty stubs.

## Key Files

| File | Purpose | Notes |
|------|---------|-------|
| `hugo.toml` | Site configuration | Menus, params, base URL |
| `layouts/_default/baseof.html` | Base HTML template | CDN scripts, meta tags |
| `layouts/index.html` | Homepage template | Slider + card loop |
| `layouts/partials/homepage-card.html` | Card component | Handles all card types |
| `static/css/custom.css` | Modern CSS overrides | Main customization file |
| `static/layout/js/main.js` | Site JavaScript | Swiper init, legacy functions |
| `archetypes/homepage.md` | New card template | Used by `hugo new` |

## Common Tasks

### Adding a New Homepage Card Type

1. Update `layouts/partials/homepage-card.html` to handle the new type
2. Update `archetypes/homepage.md` if new front matter fields are needed
3. Update `docs/CONTENT-MANAGEMENT.md` with instructions
4. Create an example card in `content/homepage/`

### Modifying Styles

1. Add CSS to `static/css/custom.css`
2. Use existing CSS Custom Properties from `:root` where possible
3. Follow the existing section organization in the file
4. Test responsive breakpoints (960px, 768px, 480px)

### Adding New Pages

1. Create content file in `content/` (e.g., `content/about.md`)
2. Create layout if needed in `layouts/_default/` or `layouts/`
3. Add to menu in `hugo.toml` if navigation is needed

### Updating External Libraries

CDN resources in `baseof.html` use SRI hashes. To update:

1. Get new CDN URL for the library
2. Generate SRI hash: `curl -s [URL] | openssl dgst -sha256 -binary | openssl base64`
3. Update both the `src` and `integrity` attributes

## Code Style Guidelines

### Hugo Templates

```html
{{/* Use block comments for explanations */}}
{{ $variable := .Params.field }}

{{/* Indent nested blocks */}}
{{ if $condition }}
    {{ range .Items }}
        <div>{{ .Title }}</div>
    {{ end }}
{{ end }}
```

### CSS

```css
/* Use CSS Custom Properties for values that repeat */
.element {
    color: var(--color-text);
    margin-bottom: var(--spacing-md);
}

/* Group related rules, use section comments */
/* ==========================================================================
   Section Name
   ========================================================================== */
```

### JavaScript

```javascript
// Use jQuery for DOM manipulation (site convention)
jQuery(document).ready(function() {
    // Initialize components
});

// Prefer function declarations for named functions
function initComponent() {
    // Implementation
}
```

## Testing Checklist

Before submitting changes:

- [ ] Site builds without errors (`hugo`)
- [ ] Homepage displays correctly
- [ ] Cards render properly (image, video, text-only types)
- [ ] Slider works with navigation arrows
- [ ] Responsive layout works at all breakpoints
- [ ] No JavaScript console errors
- [ ] Links work (internal and external)
- [ ] Images have alt text
- [ ] Keyboard navigation works (Tab through page)

## AI Assistant Guidelines

When working on this project:

### Do

- Read existing files before making changes
- Follow established patterns in the codebase
- Keep changes focused and minimal
- Update documentation when adding features
- Use CSS Grid for layouts (not JavaScript-based solutions)
- Prefer CSS solutions over JavaScript when possible
- Test changes work with Hugo server before completing

### Don't

- Modify `static/layout/style.css` (use `custom.css` instead)
- Remove legacy function stubs in `main.js` (they may be called elsewhere)
- Add new JavaScript frameworks without discussion
- Create overly complex solutions for simple problems
- Forget to update SRI hashes when changing CDN resources

### Context to Gather

When starting work, understand:

1. Current state of `hugo.toml` for site configuration
2. Template structure in `layouts/`
3. Existing CSS patterns in `static/css/custom.css`
4. Content structure in `content/homepage/`

### Common Gotchas

1. **Hugo caching**: Delete `public/` folder and restart server if changes don't appear
2. **SRI hash mismatch**: Browser blocks scripts with wrong integrity hashes
3. **Front matter format**: Use YAML (not TOML) in content files
4. **Image paths**: Start with `/images/` (not `images/` or `./images/`)
5. **jQuery availability**: Scripts in templates run before jQuery loads (use `main.js` for initialization)

## Human Contributor Guidelines

### Getting Started

1. Install Hugo: https://gohugo.io/installation/
2. Clone the repository
3. Run `hugo server` for local development
4. Make changes in a feature branch
5. Test thoroughly before submitting

### Content Editing

For content changes only (no code), see [docs/CONTENT-MANAGEMENT.md](docs/CONTENT-MANAGEMENT.md).

### Development Workflow

1. Create a branch for your changes
2. Make focused, atomic commits
3. Test locally with `hugo server`
4. Ensure no build errors with `hugo`
5. Submit changes for review

### Questions?

- Check existing code for patterns and conventions
- Review Hugo documentation: https://gohugo.io/documentation/
- Look at similar implementations in the codebase

## Version History

| Date | Change |
|------|--------|
| Jan 2026 | Initial Hugo site creation |
| Jan 2026 | Replaced Flexslider with Swiper.js |
| Jan 2026 | Replaced Isotope with CSS Grid |
| Jan 2026 | Added content management documentation |
| Jan 2026 | Added kids/ and youth/ card-based sections |
| Jan 2026 | Fixed subdirectory deployment (relURL) |
| Jan 2026 | Created calendar page |

---

## Session Log (Jan 19, 2026)

### Completed Tasks

1. **Added image captions on kids/youth pages**
   - Modified `layouts/partials/homepage-card.html` to show tags even for image-only cards
   - Changed condition from `{{ if $hasContent }}` to `{{ if or $hasContent $hasTags }}`

2. **Fixed contact page SEND MESSAGE button styling**
   - Updated button CSS in `static/css/custom.css` to match original site's `general_button_type_3`

3. **Created calendar page**
   - Added `content/calendar.md` with embedded Google Calendar iframe
   - Added responsive CSS for `.responsiveCal` in `custom.css`

4. **Fixed subdirectory deployment paths**
   - Site is hosted at `https://www.minnehaha.org`
   - Updated ALL templates to use `| relURL` for paths (images, CSS, JS, links)
   - Files updated:
     - `layouts/_default/baseof.html` - favicon, CSS, JS
     - `layouts/partials/header.html` - all nav links, logo
     - `layouts/partials/footer.html` - quick links
     - `layouts/index.html` - slider images
     - `layouts/partials/homepage-card.html` - card images/videos/links
     - `layouts/_default/single.html` - banner, featured, video, downloads
     - `layouts/_default/section-with-cards.html` - banner, video
     - `layouts/_default/staff.html` - staff photos
     - `layouts/_default/contact.html` - staff photo/links

5. **Fixed GitHub Actions baseURL override**
   - `.github/workflows/hugo.yaml` was overriding `hugo.toml` baseURL with `${{ steps.pages.outputs.base_url }}`
   - Removed the `--baseURL` flag so Hugo uses `hugo.toml` setting

### Pending Verification

After `git push`:
- [ ] Verify GitHub Actions build succeeds
- [ ] Verify all images load on deployed site
- [ ] Verify all CSS/JS loads (no 404s in console)
- [ ] Verify navigation links work (include `/mumc-hugo/` prefix)
- [ ] Test kids and youth pages show captions under images

### Key Configuration

```toml
# hugo.toml
baseURL = 'https://www.minnehaha.org'
```

### Important Notes

- **Subdirectory Deployment**: When hosting Hugo in a subdirectory, ALL paths in templates must use `| relURL` to prepend the base path
- **GitHub Actions**: Don't override baseURL in workflow if hugo.toml has correct setting
- **Cloudflare Errors**: CSP warnings from Google Calendar iframe are normal; Cloudflare beacon errors are from hosting config, not Hugo

---

*This file is intended to help both AI coding assistants and human contributors work effectively on this project.*
