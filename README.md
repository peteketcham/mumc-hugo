# Minnehaha United Methodist Church Website

A Hugo-based static website for Minnehaha United Methodist Church, located in Minneapolis, MN.

## Overview

This website is built with [Hugo](https://gohugo.io/), a fast static site generator. The site features:

- **Content-driven homepage** with modular card components
- **Modern CSS** using CSS Grid and CSS Custom Properties
- **Responsive design** that works on desktop, tablet, and mobile
- **Accessibility-first** approach with skip links, focus states, and ARIA labels
- **Swiper.js** for the image carousel slider

## Quick Start

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended version recommended)

### Development

```bash
# Start the development server
hugo server

# Start with drafts visible
hugo server -D

# Build for production
hugo
```

The development server runs at `http://localhost:1313` by default.

## Project Structure

```
mumc/
├── archetypes/           # Content templates
│   └── homepage.md       # Template for homepage cards
├── content/
│   ├── homepage/         # Homepage card content files
│   └── archive.md        # Archive page
├── docs/
│   └── CONTENT-MANAGEMENT.md  # Guide for content editors
├── layouts/
│   ├── _default/
│   │   ├── baseof.html   # Base template
│   │   └── archive.html  # Archive page template
│   ├── partials/
│   │   ├── header.html   # Site header
│   │   ├── footer.html   # Site footer
│   │   └── homepage-card.html  # Card component
│   └── index.html        # Homepage template
├── static/
│   ├── css/
│   │   └── custom.css    # Custom styles (CSS Grid, Swiper, etc.)
│   ├── documents/        # PDFs and downloadable files
│   ├── images/           # Image assets
│   └── layout/           # Legacy theme CSS and JS
├── hugo.toml             # Hugo configuration
├── AGENTS.md             # AI/contributor guidelines
└── README.md             # This file
```

## Homepage Content Management

The homepage displays content "cards" loaded from Markdown files in `content/homepage/`. Each card can contain:

- An image with optional text and link
- A video with optional text
- Text only

See [docs/CONTENT-MANAGEMENT.md](docs/CONTENT-MANAGEMENT.md) for detailed instructions on managing homepage content.

### Quick Example

Create a new file `content/homepage/my-announcement.md`:

```markdown
---
title: "My Announcement"
weight: 50
image: "/images/my-photo.jpg"
image_alt: "Description of the photo"
link: "https://example.com"
external: true
---

**Announcement text** goes here with [links](https://example.com) and formatting.
```

### Card Settings

| Setting | Description |
|---------|-------------|
| `title` | Internal name (not displayed) |
| `weight` | Display order (lower = first) |
| `draft` | Set `true` to hide temporarily |
| `archived` | Set `true` to move to archive page |
| `image` | Path to image file |
| `image_alt` | Accessibility description |
| `video` | Path to video file (MP4) |
| `link` | URL for clickable image |
| `external` | Set `true` for external links |

## Technology Stack

### Current (Modern)

- **Hugo** - Static site generator
- **CSS Grid** - Layout system (replaces Isotope)
- **CSS Custom Properties** - Theming and consistency
- **Swiper.js 11** - Touch-friendly image carousel
- **jQuery 3.7.1** - DOM manipulation (legacy dependency)

### Legacy (From Original Theme)

The site uses a purchased theme with legacy CSS (`static/layout/style.css`). The `static/css/custom.css` file provides modern overrides without modifying the original theme files.

## External Dependencies (CDN)

| Library | Version | Purpose |
|---------|---------|---------|
| jQuery | 3.7.1 | DOM manipulation |
| Swiper | 11.x | Image carousel |

All CDN resources include Subresource Integrity (SRI) hashes for security.

## Accessibility

The site includes:

- Skip link for keyboard navigation
- Focus states meeting WCAG 2.1 contrast requirements
- Reduced motion support (`prefers-reduced-motion`)
- Semantic HTML structure
- Alt text for images
- ARIA labels for interactive elements

## Configuration

Site settings are in `hugo.toml`:

```toml
baseURL = 'https://minnehaha.org/'
title = 'Minnehaha United Methodist Church'

[params]
  description = "Your neighborhood church in Minneapolis"
  address = "3701 East 50th Street, Minneapolis, MN 55417"
  phone = "612.721.6231"
  email = "office@minnehaha.org"
```

## Deployment

Build the site for production:

```bash
hugo --minify
```

The built site will be in the `public/` directory, ready to deploy to any static hosting service.

## Contributing

See [AGENTS.md](AGENTS.md) for guidelines on contributing to this project, including information for both human developers and AI coding assistants.

## License

This website is property of Minnehaha United Methodist Church. The Hugo framework and third-party libraries are subject to their respective licenses.

---

**Minnehaha United Methodist Church**
3701 East 50th Street, Minneapolis, MN 55417
612.721.6231 | office@minnehaha.org
