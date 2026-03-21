[Back to README](../README.md) · [Templates & Customization -->](templates.md)

# Getting Started

A detailed walkthrough of the 5-step wizard for creating your landing page.

## Prerequisites

- A modern web browser (Chrome, Firefox, Safari, Edge)
- No server, no Node.js, no build tools required

## Opening the Generator

**Option 1 — Online:**
Visit [https://vkrasnovid.github.io/landing-generator/](https://vkrasnovid.github.io/landing-generator/)

**Option 2 — Local:**
```bash
git clone https://github.com/vkrasnovid/landing-generator.git
open landing-generator/index.html
```

The interface has two panels: the wizard form (left) and live preview (right). On mobile, they stack vertically.

## Step-by-Step Wizard

### Step 1: Company Info

| Field | Required | Description |
|-------|----------|-------------|
| Company Name | Yes | Appears in hero, header, footer, and meta tags |
| Slogan | No | Subtitle displayed below the company name in the hero section |
| Description | No | About section text (2-3 sentences recommended) |

### Step 2: Services

Add up to **8 service cards**. Each card has:

- **Icon** — click the icon button to open the emoji picker (30+ business icons)
- **Service Name** — short title (e.g., "Web Development")
- **Description** — brief explanation of the service

Click **"+ Add Service"** to add more cards. Click **"Delete"** on any card to remove it.

### Step 3: Team

Add up to **6 team members**. Each entry has:

- **Name** — team member's full name (required per entry)
- **Role** — job title or position
- **Description** — short bio

### Step 4: Contacts

| Field | Format |
|-------|--------|
| Phone | +7 (999) 000-00-00 |
| Email | info@company.ru |
| Address | Free text |
| VKontakte | https://vk.com/... |
| Telegram | @username |
| Website | https://example.ru |

At least one contact method is recommended. All fields are optional.

### Step 5: Style

Three choices to make:

1. **Template** — Classic, Minimal, or Corporate (see [Templates & Customization](templates.md))
2. **Color Preset** — 5 built-in palettes, or use the custom color picker
3. **Hero Photo** — browse 6 categories of Unsplash photos (business, law, medicine, IT, food, auto)

## Preview & Export

The right panel shows a **live preview** that updates as you type (300ms debounce).

**Controls:**
- **Desktop/Mobile toggle** — switch preview between full-width and 375px mobile view
- **Download HTML** — saves a self-contained `.html` file named `{company}-landing.html`
- **Copy Code** — copies the full HTML to clipboard (shows "Copied!" confirmation)

The downloaded file has zero external dependencies — all CSS is inlined, all images are Unsplash URLs. Open it in any browser or upload to any static hosting.

## See Also

- [Templates & Customization](templates.md) — detailed template comparison and color options
