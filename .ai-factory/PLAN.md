# Implementation Plan: Landing Page Generator

Branch: none (fast mode)
Created: 2026-03-20

## Settings
- Testing: no
- Logging: verbose
- Docs: no

## Commit Plan
- **Commit 1** (after tasks 1-3): "feat: add wizard form with all steps and state management"
- **Commit 2** (after tasks 4-6): "feat: add three landing templates with HTML generator engine"
- **Commit 3** (after tasks 7-9): "feat: add preview iframe, download button, icon/photo library and dark UI polish"

## Tasks

### Phase 1: Project Bootstrap & Wizard Form

- [x] Task 1: Create base `index.html` structure with dark UI shell

  Build the single-file skeleton: `<!DOCTYPE html>` with dark-theme CSS variables, the two-panel
  layout (left = wizard form, right = live preview iframe), and a minimal JS app object.

  Details:
  - Dark theme: `--bg: #0f0f0f`, `--surface: #1a1a1a`, `--accent: #6c63ff`, `--text: #e0e0e0`
  - Two-column layout: form panel (40%) | preview panel (60%)
  - All CSS inline inside `<style>`, all JS inside `<script>` at bottom of `<body>`
  - No external dependencies — 100% self-contained
  - App state object: `const APP = { step: 1, data: {}, template: 'classic' }`
  - Console logging: `console.debug('[APP] init', APP)` on page load
  - Files: `index.html`

- [x] Task 2: Implement the 5-step wizard form with progress bar and navigation

  Create the multi-step wizard with step components rendered into `#form-panel`:

  - **Step 1 — Компания:** поля `companyName` (required), `slogan`, `description` (textarea)
  - **Step 2 — Услуги:** до 8 карточек, кнопки "+ Добавить услугу" / "Удалить"; каждая карточка:
    `serviceName`, `serviceDesc`, `serviceIcon` (emoji-picker, минимум 30 вариантов)
  - **Step 3 — Команда:** до 6 человек; каждый: `memberName`, `memberRole`, `memberDesc`
  - **Step 4 — Контакты:** поля `phone`, `email`, `address`, `vk`, `telegram`, `website`
  - **Step 5 — Стиль:** выбор шаблона (Classic / Minimal / Corporate) + 5 цветовых пресетов +
    custom color picker для primary цвета

  Progress bar: step indicator `Шаг N из 5` + filled dots
  Navigation: кнопки "Назад" / "Далее" / "Сгенерировать"
  Validation: required fields highlighted on empty, no step advance without filling required fields
  State persistence: all inputs sync to `APP.data` via `input` event listeners

  Logging:
  - `console.debug('[WIZARD] step changed', { from, to })` on each navigation
  - `console.debug('[WIZARD] field updated', { field, value })` on input
  - `console.warn('[WIZARD] validation failed', { step, missing })` on failed advance

  Files: `index.html` (JS wizard functions + CSS step styles)

- [x] Task 3: Icon picker component and hero photo selector

  Inline icon/photo assets so the file stays self-contained:

  - **Icon picker** (Task 2 Step 2): emoji grid — minimum 30 business emoji icons
    (🏢 🏗 ⚖️ 💼 🩺 💻 🚗 🍽 📊 🔧 🏠 ✈️ 📱 💰 🎓 🔬 📋 🛡 🌐 🤝 📈 🎨 🔑 📦 🚀 💡 🏋️ 🌿 🎵 ⚙️)
  - **Hero photo selector** (Task 5 Step 5): 6 categories × 3 Unsplash URLs each:
    бизнес, юриспруденция, медицина, IT, еда, авто
    (store as object with category → array of `{ url, thumb, label }`)
  - Clicking an emoji/photo sets it in `APP.data` and re-renders preview

  Logging:
  - `console.debug('[ICONS] selected', { icon, serviceIndex })` on icon pick
  - `console.debug('[PHOTOS] selected', { category, url })` on photo pick

  Files: `index.html`

<!-- Commit checkpoint: tasks 1-3 — "feat: add wizard form with all steps and state management" -->

### Phase 2: Landing Templates & HTML Generator Engine

- [x] Task 4: Build the "Classic" landing template

  JS template literal function `templates.classic(data)` → returns full HTML string.

  Sections (all in Russian placeholder text where user left fields empty):
  - **Hero:** полноэкранный, overlay поверх hero-фото, название компании + слоган + CTA кнопка
  - **About:** двухколоночный, текст описания слева, фото справа
  - **Services:** grid 2×N карточек с иконкой + заголовком + описанием
  - **Team:** карточки участников (имя, должность, краткое bio)
  - **Reviews:** блок из 2-3 заглушек-отзывов (если нет реальных данных — hidden)
  - **Contacts:** адрес, телефон, email, иконки соцсетей
  - **Footer:** копирайт с названием компании

  Responsive: мобильные breakpoints в inline `<style>` внутри сгенерированного HTML
  Primary color: подставляется из `APP.data.primaryColor`

  Logging:
  - `console.debug('[TEMPLATE:classic] generating', data)` on entry
  - `console.debug('[TEMPLATE:classic] done, length', html.length)` on exit

  Files: `index.html` (JS template function)

- [x] Task 5: Build the "Minimal" and "Corporate" landing templates

  **Minimal** — `templates.minimal(data)`:
  - Белый фон, большие шрифты (headline ≥ 64px), минимум декора
  - Однострочные секции, много whitespace
  - Нет фоновых изображений (только текст + иконки)

  **Corporate** — `templates.corporate(data)`:
  - Строгий стиль, синие тона (overridden primary #1a3a6b if no custom color)
  - Таблица услуг вместо карточек
  - Блок "Ключевые факты в цифрах" (если заполнены поля в Step 1 description — парсим числа,
    иначе заглушки: "10+ лет", "500+ клиентов", "24/7 поддержка")
  - Строгий header + footer с контрастной полосой

  Оба шаблона: responsive, все стили inline в `<style>`, все скрипты inline

  Logging:
  - `console.debug('[TEMPLATE:minimal] generating', data)`
  - `console.debug('[TEMPLATE:corporate] generating', data)`

  Files: `index.html`

- [x] Task 6: HTML generator engine — compose final output HTML

  Function `generateHTML(data, templateName)` → full self-contained HTML string:

  1. Call `templates[templateName](data)` to get template HTML
  2. Inject `<meta>` tags: `title`, `description`, OG `title`/`description`/`image`
  3. Apply selected color scheme: replace CSS variable `--primary` with `data.primaryColor`
  4. Apply color preset if chosen (5 presets: фиолетовый, синий, зелёный, красный, тёмный)
  5. Substitute all icons and hero photo URL into template placeholders
  6. Return final string — must be a valid, openable `.html` file with zero external deps

  Called on every wizard change to keep preview live.

  Logging:
  - `console.debug('[GENERATOR] start', { template: templateName, dataKeys: Object.keys(data) })`
  - `console.debug('[GENERATOR] meta injected')`
  - `console.debug('[GENERATOR] colors applied', { primary: data.primaryColor })`
  - `console.debug('[GENERATOR] output size', output.length)`
  - `console.error('[GENERATOR] error', err)` on any exception

  Files: `index.html`

<!-- Commit checkpoint: tasks 4-6 — "feat: add three landing templates with HTML generator engine" -->

### Phase 3: Preview, Download & UI Polish

- [x] Task 7: Live preview iframe + desktop/mobile switcher

  Right panel `#preview-panel`:
  - `<iframe id="preview-frame">` updates via `srcdoc` attribute on every data change
  - Debounce update: 300ms after last input change
  - Desktop/mobile switcher: two buttons toggle iframe width (100% vs 375px centered)
  - Template selector tabs above iframe: "Классический" | "Минималистичный" | "Корпоративный"
  - On template switch → regenerate and update `srcdoc`

  Logging:
  - `console.debug('[PREVIEW] update triggered, srcdoc length', html.length)`
  - `console.debug('[PREVIEW] mode switched', { mode })` on desktop/mobile toggle
  - `console.debug('[PREVIEW] template switched', { template })`

  Files: `index.html`

- [x] Task 8: Download HTML and Copy Code buttons

  Two action buttons in the top-right of the preview panel:

  - **"Скачать HTML"**: creates a `Blob` with `text/html`, makes a temporary `<a>` with
    `download="landing.html"`, clicks it, then revokes the object URL
  - **"Копировать код"**: `navigator.clipboard.writeText(html)`, then shows a short
    "Скопировано!" tooltip for 2 seconds

  Both use the latest `generateHTML(APP.data, APP.template)` output.

  Logging:
  - `console.debug('[DOWNLOAD] triggered, size', html.length)`
  - `console.debug('[COPY] triggered')`
  - `console.error('[COPY] clipboard error', err)` on failure

  Files: `index.html`

- [x] Task 9: Dark UI polish — transitions, animations, mobile-friendly

  Final visual pass on the generator UI itself:

  - Smooth step transitions: `opacity` + `transform: translateX` CSS transitions (300ms ease)
  - Generation spinner: spinning circle overlay shown for 200ms during `generateHTML` call
  - Active step dot in progress bar pulses with `@keyframes pulse`
  - All UI labels, placeholders, tooltips, error messages — **100% Russian**
  - Mobile layout: below 768px, stack form panel above preview panel (full width)
  - Scrollable form panel independently of preview panel
  - Hover states on all interactive elements (buttons, cards, icon picker cells)

  Logging:
  - `console.debug('[UI] transition start', { step })`
  - `console.debug('[UI] spinner shown/hidden')`

  Files: `index.html`

<!-- Commit checkpoint: tasks 7-9 — "feat: add preview iframe, download, icon library and dark UI polish" -->
