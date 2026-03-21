# Landing Page Generator

> Create professional landing pages in minutes — no coding required.

A browser-based tool with a 5-step wizard that generates fully self-contained HTML landing pages. Pick a template, fill in your company details, customize colors, and download a ready-to-deploy `.html` file.

**[Live Demo](https://vkrasnovid.github.io/landing-generator/)**

## Quick Start

No installation needed — it runs entirely in the browser.

```
# Clone and open locally
git clone https://github.com/vkrasnovid/landing-generator.git
open landing-generator/index.html
```

Or just visit the [live demo](https://vkrasnovid.github.io/landing-generator/).

## Key Features

- **5-Step Wizard** — guided form: company info, services, team, contacts, style
- **3 Templates** — Classic (hero + sections), Minimal (clean whitespace), Corporate (formal tables + stats)
- **Live Preview** — instant iframe preview updates as you type, with desktop/mobile toggle
- **Color Customization** — 5 color presets + custom color picker
- **Hero Photos** — built-in Unsplash photo library across 6 categories
- **30+ Icons** — emoji icon picker for services
- **Download & Copy** — export as `.html` file or copy code to clipboard
- **Zero Dependencies** — single `index.html` file, ~2100 lines, no build step

## How It Works

1. **Company** — enter name, slogan, and description
2. **Services** — add up to 8 service cards with icons
3. **Team** — add up to 6 team members
4. **Contacts** — phone, email, address, social links
5. **Style** — choose template, color scheme, and hero photo

Click **"Generate"** to download a self-contained HTML landing page with all styles inlined.

## Templates

| Template | Style | Best For |
|----------|-------|----------|
| Classic | Full-screen hero, card grid, overlay sections | General business, agencies |
| Minimal | White background, large typography, lots of whitespace | Creative studios, portfolios |
| Corporate | Formal layout, data tables, key facts in numbers | Law firms, consulting, finance |

All templates are responsive (mobile + desktop) with inline CSS — no external dependencies.

---

## Documentation

| Guide | Description |
|-------|-------------|
| [Getting Started](docs/getting-started.md) | Detailed usage walkthrough for each wizard step |
| [Templates & Customization](docs/templates.md) | Template details, color presets, and hero photos |

## Tech Stack

- **Single file:** `index.html` with inline `<style>` and `<script>`
- **No frameworks:** vanilla HTML, CSS, JavaScript
- **Hosting:** GitHub Pages (static)
- **UI:** dark theme with CSS variables, smooth transitions

## License

MIT
