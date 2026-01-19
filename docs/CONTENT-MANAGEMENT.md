# Homepage Content Management Guide

This guide explains how to add, edit, and archive content cards on the Minnehaha UMC website homepage.

## Overview

The homepage displays a series of "cards" - each card can contain:
- An image with optional text and link
- A video with optional text
- Text only (no image or video)

Each card is a separate file in the `content/homepage/` folder. The website automatically displays all non-archived cards, sorted by their "weight" (display order).

---

## Quick Reference

| Task | Action |
|------|--------|
| Add new card | Create a new `.md` file in `content/homepage/` |
| Edit a card | Open and modify the existing `.md` file |
| Change display order | Change the `weight` value (lower = appears first) |
| Hide temporarily | Set `draft: true` |
| Archive permanently | Set `archived: true` |
| Delete | Remove the file (or archive it instead) |

---

## Understanding Card Files

Each card is a Markdown file (`.md`) with two parts:

1. **Front Matter** - Settings between `---` marks at the top
2. **Content** - The text that appears below the image/video

### Example Card File

```markdown
---
title: "Join Us For Worship"
weight: 10
draft: false
archived: false
image: "/images/SUMMER-2022-WORSHIP.jpg"
image_alt: "Join us for worship at 9:30 a.m."
link: "https://www.youtube.com/@MinnehahaUMC"
external: true
---

**JOIN US FOR WORSHIP THIS SUNDAY:** All services are livestreamed...
```

---

## Front Matter Settings Explained

### Required Settings

| Setting | What It Does | Example |
|---------|--------------|---------|
| `title` | Internal name for the card (not shown on site) | `"Sunday Worship"` |
| `weight` | Display order (lower numbers appear first) | `10`, `50`, `100` |

### Optional Settings

| Setting | What It Does | Example |
|---------|--------------|---------|
| `draft` | If `true`, card is hidden from the site | `false` |
| `archived` | If `true`, card moves to archive page | `false` |
| `image` | Path to the image file | `"/images/my-image.jpg"` |
| `image_alt` | Description of image for accessibility | `"Church building"` |
| `video` | Path to video file (MP4) | `"/images/welcome.mp4"` |
| `link` | URL when clicking the image | `"https://example.com"` |
| `external` | If `true`, link opens in new tab with arrow icon | `true` |

---

## Common Tasks

### Adding a New Card

1. **Create a new file** in the `content/homepage/` folder
   - Name it something descriptive, like `spring-concert.md`
   - Use lowercase letters and hyphens (no spaces)

2. **Copy this template** and paste it into your new file:

```markdown
---
title: "Your Card Title"
weight: 100
draft: false
archived: false
image: "/images/your-image.jpg"
image_alt: "Description of the image"
link: ""
external: false
---

Your text content goes here. You can use **bold** and *italic* text.
```

3. **Customize the settings**:
   - Change the `title` to something descriptive
   - Set the `weight` to control where it appears (see "Display Order" below)
   - Add your image path, or remove the `image` line for text-only
   - Add your content text below the `---`

4. **Upload your image** (if using one):
   - Place the image in the `static/images/` folder
   - Use the path `/images/filename.jpg` in your card

### Editing an Existing Card

1. Open the card file in `content/homepage/`
2. Make your changes to the front matter or content
3. Save the file

### Changing Display Order

Cards appear in order by their `weight` value (lowest first).

**Suggested weight ranges:**
- `10-90`: Top of page (important announcements)
- `100-190`: Upper section
- `200-290`: Middle section
- `300-390`: Lower section
- `400+`: Bottom of page

**Example:** To move a card to the top:
```yaml
weight: 15
```

**Tip:** Leave gaps between weight numbers (10, 20, 30...) so you can insert new cards without renumbering everything.

### Hiding a Card Temporarily

Set `draft: true` in the front matter:

```yaml
draft: true
```

The card will be hidden from the website but the file remains for later use.

### Archiving a Card

When an announcement is no longer current but you want to keep it for reference:

```yaml
archived: true
```

Archived cards appear on the `/archive/` page instead of the homepage.

### Deleting a Card

Simply delete the file from `content/homepage/`. However, consider archiving instead so you have a record of past announcements.

---

## Card Types

### Image Card with Text

Shows an image at the top with text below. Optionally, the image can link somewhere.

```markdown
---
title: "Event Announcement"
weight: 50
image: "/images/event-photo.jpg"
image_alt: "People at the community event"
link: "https://example.com/register"
external: true
---

Join us for our annual community gathering! Click the image above to register.
```

### Image Card without Text

Shows only an image (no text below).

```markdown
---
title: "Banner Image"
weight: 25
image: "/images/banner.jpg"
image_alt: "Welcome to Minnehaha UMC"
---
```

### Video Card

Shows a video player with optional text below.

```markdown
---
title: "Welcome Video"
weight: 20
video: "/images/welcome-video.mp4"
---

Watch our welcome message from Pastor Becky.
```

### Text-Only Card

Shows only text (useful for newsletters, announcements without images).

```markdown
---
title: "Newsletter Links"
weight: 380
---

### CHURCH NEWSLETTERS

[Click here for the January newsletter.](/documents/january-newsletter.pdf)
[Click here for the December newsletter.](/documents/december-newsletter.pdf)
```

---

## Formatting Text Content

The content below the `---` uses Markdown formatting:

| Format | How to Write It | Result |
|--------|-----------------|--------|
| Bold | `**bold text**` | **bold text** |
| Italic | `*italic text*` | *italic text* |
| Link | `[text](https://url.com)` | [text](https://url.com) |
| Heading | `### Heading Text` | Large heading |
| Line break | Empty line between paragraphs | New paragraph |

### Example with Formatting

```markdown
---
title: "Special Announcement"
weight: 30
image: "/images/announcement.jpg"
image_alt: "Special event"
---

**MARK YOUR CALENDARS!** Our annual celebration is coming up.

Join us on *Saturday, March 15th* for food, fellowship, and fun.

[Click here to sign up](https://signup.example.com) or contact the office.
```

---

## Adding Images

1. **Prepare your image:**
   - Use JPG or PNG format
   - Recommended width: 600-1200 pixels
   - Keep file size reasonable (under 500KB if possible)

2. **Name your file:**
   - Use lowercase letters and hyphens
   - Example: `spring-concert-2024.jpg`

3. **Upload to the images folder:**
   - Place the file in `static/images/`

4. **Reference in your card:**
   ```yaml
   image: "/images/spring-concert-2024.jpg"
   ```

---

## Uploading Documents (PDFs)

For newsletters and other documents:

1. Place the file in `static/documents/`
2. Link to it in your content:
   ```markdown
   [Download the newsletter](/documents/newsletter-january-2024.pdf)
   ```

---

## Troubleshooting

### Card not showing up?
- Check that `draft` is `false` (or not present)
- Check that `archived` is `false` (or not present)
- Make sure the file is in `content/homepage/` folder
- Verify the file ends in `.md`

### Image not displaying?
- Check the path starts with `/images/`
- Verify the image file is in `static/images/`
- Make sure the filename matches exactly (case-sensitive)

### Card in wrong position?
- Adjust the `weight` value
- Lower numbers appear first

### Text formatting looks wrong?
- Make sure there's a blank line after the `---`
- Check Markdown syntax (use `**` for bold, `*` for italic)

---

## File Naming Conventions

When creating new card files:

- Use lowercase letters
- Use hyphens instead of spaces
- Keep names short but descriptive
- End with `.md`

**Good examples:**
- `easter-service.md`
- `food-shelf-update.md`
- `summer-2024-worship.md`

**Avoid:**
- `Easter Service.md` (spaces and capitals)
- `announcement.md` (too vague)
- `new-card-1.md` (not descriptive)

---

## Need Help?

If you're unsure about making changes:

1. Look at existing card files for examples
2. Make a backup copy of any file before editing
3. Test changes on the development server before publishing
4. Contact the website administrator for assistance

---

*Last updated: January 2026*
