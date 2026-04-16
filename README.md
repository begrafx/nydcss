# nydcss

**A modern, composable CSS framework** that synthesizes the strongest ideas from 20+ leading CSS projects into one cohesive, zero-dependency stylesheet.

---

## What it is

nydcss combines:

| Source | What we took |
|--------|-------------|
| **normalize.css / sanitize.css** | Opinionated cross-browser reset baseline |
| **water.css / beer.css** | Classless semantic HTML styling |
| **Tailwind CSS** | Utility-first design language, spacing/color scales |
| **UnoCSS / Windi CSS** | On-demand philosophy, variant groups, attributify patterns |
| **Bootstrap** | Battle-tested component patterns, responsive grid |
| **Bulma** | Clean flexbox column system, modifier naming |
| **halfmoon.css** | First-class dark mode with CSS custom properties |
| **mini.css / Chalarangelo** | Compact, accessible component defaults |
| **Tachyons** | Single-responsibility, immutable utility classes |
| **animate.css / animae.css** | Polished keyframe animation library |
| **PureCSS** | Lightweight grid and form primitives |
| **AstroTurf CSS** | Scoped CSS philosophy |
| **CSS Bliss / css-bliss** | BEM-flavored, intentional class naming |
| **Airbnb CSS Guide** | Formatting and architecture conventions |
| **Addyosmani/critical** | Critical CSS extraction mindset — modular `@import` |
| **filamentgroup/loadCSS** | Progressive CSS loading awareness |
| **OptiCSS (LinkedIn)** | Class reuse efficiency, minimal specificity |
| **PreCSS / Stylus** | CSS custom property token system as the "preprocessor" |
| **select-css** | Normalized cross-platform form element styling |
| **sugarss** | Concise, readable rule authoring style |

---

## Quick Start

### CDN (fastest)

```html
<link rel="stylesheet" href="https://unpkg.com/nydcss/dist/nyd.css">
```

Minified:
```html
<link rel="stylesheet" href="https://unpkg.com/nydcss/dist/nyd.min.css">
```

### npm

```bash
npm install nydcss
```

```css
/* Import everything */
@import "nydcss/dist/nyd.css";

/* Or import only what you need (modular) */
@import "nydcss/src/nyd-tokens.css";
@import "nydcss/src/nyd-reset.css";
@import "nydcss/src/nyd-layout.css";
@import "nydcss/src/nyd-components.css";
```

---

## Architecture

```
nydcss/
├── src/
│   ├── nyd-tokens.css      # CSS custom properties (design tokens)
│   ├── nyd-reset.css       # Reset + normalize
│   ├── nyd-base.css        # Semantic HTML base styles + .nyd-prose
│   ├── nyd-layout.css      # Container, flex, grid, stack, sidebar
│   ├── nyd-utilities.css   # Spacing, sizing, color, border, shadow
│   ├── nyd-components.css  # Buttons, forms, cards, nav, modals...
│   ├── nyd-animations.css  # Keyframes + animation utilities
│   └── nyd-responsive.css  # Responsive variants + helpers
├── dist/
│   ├── nyd.css             # Full build (~108kb uncompressed)
│   └── nyd.min.css         # Minified (~69kb, ~17kb gzip)
└── examples/
    └── index.html          # Full component showcase
```

---

## Design Tokens

Everything is a CSS custom property. Override at `:root` or any scope:

```css
/* Custom theme */
:root {
  --nyd-color-primary:       #7c3aed;   /* purple */
  --nyd-color-primary-hover: #6d28d9;
  --nyd-font-sans: "Inter", system-ui, sans-serif;
  --nyd-radius-lg: 12px;                /* rounder corners */
}

/* Scoped theme */
.my-component {
  --nyd-color-primary: #0ea5e9;
}
```

### Key token groups

```css
/* Typography */
--nyd-font-sans / --nyd-font-serif / --nyd-font-mono
--nyd-text-xs ... --nyd-text-6xl        /* font sizes */
--nyd-font-normal / --nyd-font-bold     /* weights */
--nyd-leading-tight / --nyd-leading-relaxed

/* Spacing */
--nyd-space-1 (4px) ... --nyd-space-64 (256px)

/* Color semantic aliases */
--nyd-color-primary / --nyd-color-success / --nyd-color-warning / --nyd-color-danger
--nyd-color-text / --nyd-color-text-muted / --nyd-color-bg
--nyd-color-surface / --nyd-color-surface-2 / --nyd-color-border

/* Shadows */
--nyd-shadow-xs ... --nyd-shadow-2xl

/* Transitions */
--nyd-duration-fast (100ms) / --nyd-duration-base (150ms) / --nyd-duration-slow (300ms)
--nyd-ease-in / --nyd-ease-out / --nyd-ease-inout / --nyd-ease-spring

/* Z-index */
--nyd-z-sticky (100) / --nyd-z-modal (400) / --nyd-z-toast (500) / --nyd-z-tooltip (600)
```

---

## Dark Mode

Automatic via `prefers-color-scheme`. Force with `data-theme`:

```html
<!-- Force dark -->
<html data-theme="dark">

<!-- Force light -->
<html data-theme="light">

<!-- System default (auto) -->
<html>
```

Toggle with JavaScript:
```js
const toggle = () => {
  const current = document.documentElement.dataset.theme;
  document.documentElement.dataset.theme = current === 'dark' ? 'light' : 'dark';
};
```

---

## Layout

### Container

```html
<div class="container">         <!-- responsive max-width -->
<div class="container-sm">     <!-- max 640px -->
<div class="container-prose">  <!-- max 65ch, readable column -->
```

### Flexbox

```html
<div class="flex items-center justify-between gap-4">
  <span>Left</span>
  <span>Right</span>
</div>
```

### Grid

```html
<!-- Fixed columns -->
<div class="grid grid-cols-3 gap-6">

<!-- Fluid auto-fit (no breakpoints needed!) -->
<div class="auto-grid-md gap-6">

<!-- Responsive with breakpoint prefix -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
```

### Stack (vertical rhythm)

```html
<div class="stack-6">
  <p>Paragraph one</p>
  <p>Paragraph two — automatically spaced 1.5rem below</p>
</div>
```

### Sidebar Layout

```html
<div class="with-sidebar">
  <aside>Sidebar (fixed width)</aside>
  <main>Main content (takes remaining space, wraps below on mobile)</main>
</div>
```

---

## Components

### Buttons

```html
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-outline">Outline</button>
<button class="btn btn-ghost">Ghost</button>
<button class="btn btn-danger">Danger</button>
<button class="btn btn-link">Link style</button>

<!-- Sizes -->
<button class="btn btn-primary btn-xs">Extra small</button>
<button class="btn btn-primary btn-sm">Small</button>
<button class="btn btn-primary btn-lg">Large</button>
<button class="btn btn-primary btn-xl">Extra large</button>

<!-- Full width -->
<button class="btn btn-primary btn-wide">Full width</button>

<!-- Loading -->
<button class="btn btn-primary btn-loading" disabled>Loading</button>

<!-- Button group -->
<div class="btn-group">
  <button class="btn btn-secondary">Left</button>
  <button class="btn btn-secondary">Mid</button>
  <button class="btn btn-secondary">Right</button>
</div>
```

### Forms

```html
<div class="form-group">
  <label class="label label-required" for="email">Email</label>
  <input class="input" type="email" id="email" placeholder="you@example.com">
  <span class="form-hint">We'll never share your email.</span>
</div>

<!-- Input group with prefix/suffix -->
<div class="input-group">
  <span class="input-group-prepend">https://</span>
  <input class="input" type="text" placeholder="your-domain.com">
</div>

<!-- Error state -->
<input class="input input-error" type="text">
<span class="form-error-msg">This field is required.</span>

<!-- Select -->
<select class="select">
  <option>Option 1</option>
</select>

<!-- Toggle switch -->
<label class="flex items-center gap-3">
  <span class="toggle">
    <input type="checkbox" checked>
    <span class="toggle-slider"></span>
  </span>
  Enable notifications
</label>
```

### Cards

```html
<div class="card card-hover">
  <img class="card-image" src="photo.jpg" alt="">
  <div class="card-body">
    <h2 class="card-title">Card title</h2>
    <p class="card-subtitle">Supporting text</p>
    <p class="mt-3 text-sm text-muted">Card body content.</p>
  </div>
  <div class="card-footer">
    <button class="btn btn-primary btn-sm">Action</button>
  </div>
</div>
```

### Alerts

```html
<div class="alert alert-info">
  <div class="alert-content">
    <p class="alert-title">Information</p>
    <p>This is an informational message.</p>
  </div>
</div>

<div class="alert alert-success"> ... </div>
<div class="alert alert-warning"> ... </div>
<div class="alert alert-danger">  ... </div>
```

### Badges

```html
<span class="badge">Default</span>
<span class="badge badge-primary">Primary</span>
<span class="badge badge-pill badge-success">Success</span>
<span class="badge badge-danger">Danger</span>
<span class="badge-dot text-success">Active</span>
```

### Navigation

```html
<nav class="navbar navbar-sticky navbar-glass">
  <a class="navbar-brand" href="/">Brand</a>
  <ul class="navbar-nav">
    <li><a href="/" class="active">Home</a></li>
    <li><a href="/docs">Docs</a></li>
    <li><a href="/about">About</a></li>
  </ul>
  <div class="navbar-spacer"></div>
  <button class="btn btn-primary btn-sm">Sign up</button>
</nav>

<!-- Tabs -->
<nav class="tabs">
  <button class="tab active">Overview</button>
  <button class="tab">Settings</button>
  <button class="tab">Activity</button>
</nav>

<!-- Breadcrumb -->
<ol class="breadcrumb">
  <li><a href="/">Home</a></li>
  <li><a href="/docs">Docs</a></li>
  <li>Components</li>
</ol>
```

### Table

```html
<div class="table-wrap">
  <table class="table table-striped table-hover table-rounded">
    <thead>
      <tr>
        <th>Name</th>
        <th>Status</th>
        <th>Date</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Alice</td>
        <td><span class="badge badge-pill badge-success">Active</span></td>
        <td>Apr 15, 2026</td>
      </tr>
    </tbody>
  </table>
</div>
```

### Progress & Spinners

```html
<!-- Progress bar -->
<div class="progress">
  <div class="progress-bar" style="width: 65%"></div>
</div>

<!-- Spinner -->
<span class="spinner"></span>
<span class="spinner spinner-sm"></span>
<span class="spinner spinner-lg"></span>
```

### Tooltip

```html
<button data-tooltip="This is a tooltip">Hover me</button>
<button data-tooltip="Tooltip below" data-tooltip-pos="bottom">Below</button>
```

### Skeleton Loader

```html
<div class="skeleton skeleton-title mb-4"></div>
<div class="skeleton skeleton-text"></div>
<div class="skeleton skeleton-text"></div>
<div class="skeleton skeleton-text mb-6"></div>
<div class="skeleton skeleton-btn"></div>
```

### Avatar

```html
<span class="avatar">AB</span>
<span class="avatar avatar-lg"><img src="user.jpg" alt="User"></span>

<!-- Avatar group -->
<div class="avatar-group">
  <span class="avatar avatar-sm">A</span>
  <span class="avatar avatar-sm">B</span>
  <span class="avatar avatar-sm">C</span>
</div>
```

### Stats / KPIs

```html
<div class="card card-body">
  <div class="stat">
    <span class="stat-label">Total Revenue</span>
    <span class="stat-value">$48,295</span>
    <span class="stat-change-up">↑ 12.5% vs last month</span>
  </div>
</div>
```

---

## Animations

```html
<!-- Continuous -->
<div class="animate-spin">...</div>
<div class="animate-pulse">...</div>
<div class="animate-bounce">...</div>
<div class="animate-float">...</div>

<!-- One-shot (trigger via JS by adding/removing class) -->
<div class="animate-fadein">...</div>
<div class="animate-slideup">...</div>
<div class="animate-scalein">...</div>
<div class="animate-shake">...</div>

<!-- Modifiers -->
<div class="animate-spin animate-slow animate-infinite">...</div>
<div class="animate-bounce animate-delay-300">...</div>
```

---

## Prose / Long-form Content

Wrap article content with `.nyd-prose` for automatic typographic styling:

```html
<article class="nyd-prose container-prose mx-auto py-12">
  <h1>Article Title</h1>
  <p>Lead paragraph...</p>
  <h2>Section heading</h2>
  <ul>
    <li>List items are styled automatically</li>
  </ul>
  <blockquote>Quotes are styled too.</blockquote>
  <pre><code>code blocks also</code></pre>
</article>
```

---

## Responsive Utilities

```html
<!-- Responsive grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3">

<!-- Hide/show at breakpoints -->
<nav class="hidden md:block">Desktop nav</nav>
<nav class="md:hidden">Mobile nav</nav>
```

---

## Critical CSS Pattern

Load only what each page needs (inspired by Addyosmani/critical + loadCSS):

```html
<!-- In <head> — inline critical styles -->
<style>
  @import "nydcss/src/nyd-tokens.css";
  @import "nydcss/src/nyd-reset.css";
  /* Only layout/tokens needed above fold */
</style>

<!-- Non-critical: load async -->
<link rel="preload" href="nydcss/dist/nyd.css" as="style"
      onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="nydcss/dist/nyd.css"></noscript>
```

---

## Customization & Theming

### Override tokens

```css
:root {
  /* Brand color */
  --nyd-color-primary:        #6d28d9;
  --nyd-color-primary-hover:  #5b21b6;
  --nyd-color-primary-light:  rgba(109,40,217,.12);
  --nyd-color-primary-alpha:  rgba(109,40,217,.2);

  /* Font */
  --nyd-font-sans: 'Inter', system-ui, sans-serif;

  /* Rounder UI */
  --nyd-radius-lg:  12px;
  --nyd-radius-xl:  16px;
  --nyd-radius-2xl: 20px;
}
```

### Scoped component theme

```css
.dashboard {
  --nyd-color-primary: #0ea5e9;
  --nyd-color-bg: #f0f9ff;
}
```

---

## File Sizes

| File | Raw | Gzip |
|------|-----|------|
| `nyd.css` | ~108 KB | ~18 KB |
| `nyd.min.css` | ~69 KB | ~13 KB |
| Tokens only | ~8 KB | ~2 KB |
| Reset only | ~4 KB | ~1.5 KB |
| Components only | ~28 KB | ~6 KB |

---

## Browser Support

All modern browsers. No IE support. Uses:
- CSS Custom Properties (variables)
- CSS Grid & Flexbox
- `aspect-ratio`
- `gap` in flexbox
- `backdrop-filter` (with fallback)
- `accent-color`
- `:focus-visible`

---

## License

MIT © nydcss contributors
