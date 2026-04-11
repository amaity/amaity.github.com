# avamaity — Design System v2.0

## Design Philosophy: Kolkata Editorial

The design language is called **Kolkata Editorial** — named after the city that sits at the intersection of South Asian intellectual life, bhadralok literary culture, and modern engineering. Think the confident typography of a 1970s Bengali literary magazine crossed with the stark layout precision of a technical journal. Bold. Literate. Personal. Not corporate.

The two sides of the site owner — power systems engineer and art-history essayist — are unified by a shared aesthetic: precision with warmth, structure with personality.

---

## Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--ink` | `#0F0E0A` | Near-black with warm brown tint. Site header background, footer background, page hero. |
| `--paper` | `#F5F0E8` | Warm cream. Body background. Not sterile white. |
| `--paper-dark` | `#EDE8DC` | Slightly darker cream. Section backgrounds, home hero. |
| `--saffron` | `#E07B39` | Warm saffron-orange. Primary accent — code block borders, post card borders, section marks, active nav. |
| `--saffron-deep` | `#B85C1A` | Deeper burnt sienna. Link color, hover on saffron. |
| `--saffron-pale` | `#FBF0E6` | Very pale saffron wash. Tag/badge backgrounds. |
| `--indigo` | `#2D3A8C` | Deep indigo-blue. Work section hero, H3 headings. |
| `--indigo-light` | `#4A5AB0` | Hover on dark indigo. |
| `--muted` | `#7A6E5F` | Warm grey. Metadata, captions, nav items (inactive), body text in hero sections. |
| `--border` | `#D8CEBC` | Warm beige. All borders and dividers. |
| `--code-bg` | `#1A1814` | Dark warm near-black. Code block backgrounds, data cards. |
| `--code-text` | `#E8E0D0` | Warm off-white. Code text color. |
| `--reading` | `#2D7A3A` | Green. Books that have been read (in books.html). |
| `--unfinished` | `#A0522D` | Sienna. Books abandoned or unfinished. |

### Why this palette?

Every developer's personal site uses blue or teal. Saffron is immediately distinctive and carries genuine cultural meaning — it appears in Indian textiles, temple pigments, manuscript illuminations. Paired with deep indigo (historically the trade commodity connecting India to Europe), the palette has intellectual grounding without being decorative.

---

## Typography

All fonts loaded via Google Fonts. One `@import` in each CSS file.

```
https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Barlow+Condensed:wght@400;600;700&family=Lora:ital,wght@0,400;0,600;1,400&family=JetBrains+Mono:wght@400&display=swap
```

| Font | Role | Weights | Why |
|------|------|---------|-----|
| **Playfair Display** | Headings, article titles, pull quotes | 700, 900, 700 italic | Editorial gravitas. High contrast thick-to-thin strokes. Dignified but not stuffy. |
| **Barlow Condensed** | Wordmark, navigation, labels, dates, tags | 400, 600, 700 | Confident, takes vertical space not horizontal. Creates editorial tension against the wide serif. |
| **Lora** | Body text in all articles and pages | 400, 400 italic, 600 | Designed for screen reading at essay length. Warmer than Georgia, less precious than EB Garamond. |
| **JetBrains Mono** | Code blocks | 400 | Superior legibility for Python; elegant curves. |

### Type scale

```css
--text-xs:   0.75rem     /* 12px — timestamps, micro-labels */
--text-sm:   0.875rem    /* 14px — navigation, captions, metadata */
--text-base: 1rem         /* 16px — body */
--text-lg:   1.125rem    /* 18px — intro paragraphs, lead text */
--text-xl:   1.375rem    /* 22px — H3 / sub-headings */
--text-2xl:  1.875rem    /* 30px — H2 */
--text-3xl:  2.5rem      /* 40px — H1 content pages */
--text-4xl:  3.5rem      /* 56px — Hero H1 */
```

---

## Spacing Scale

Based on an 8px (0.5rem) grid:

```css
--space-1:  0.25rem   /*  4px */
--space-2:  0.5rem    /*  8px */
--space-3:  0.75rem   /* 12px */
--space-4:  1rem      /* 16px */
--space-5:  1.25rem   /* 20px */
--space-6:  1.5rem    /* 24px */
--space-8:  2rem      /* 32px */
--space-10: 2.5rem    /* 40px */
--space-12: 3rem      /* 48px */
--space-16: 4rem      /* 64px */
--space-20: 5rem      /* 80px */
```

---

## Layout System

```css
--max-prose: 680px    /* Article/prose content — all body text is constrained to this */
--max-wide:  960px    /* Index pages with post cards */
--max-full: 1100px    /* Only for home hero section */
```

**Breakpoints:**
- `≥ 960px` — Full layout, side-by-side columns where applicable
- `< 960px` — Single column, some grids reflow
- `< 600px` — Tighter padding, nav condensed, hero text scaled down
- `< 380px` — Further scale-down for smallest phones

---

## Components

### Site Header

Full-width bar with background `--ink`. Contains:
- Left: `.wordmark` — site name "avamaity" in Barlow Condensed 700, `2rem`, cream (`--paper`). Turns saffron on hover.
- Right: `.site-nav` — nav items in Barlow Condensed 600 uppercase, `0.875rem`, inactive in `--muted`, active/hover in `--paper` with `2px --saffron` underline.

```html
<header class="site-header">
    <a href="index.html" class="wordmark">avamaity</a>
    <nav class="site-nav">
        <ul>
            <li class="active"><a href="#">Home</a></li>
            <li><a href="pages/pidx.html">Blog</a></li>
            <li><a href="work/widx.html">Work</a></li>
        </ul>
    </nav>
</header>
```

### Page Hero

Full-width banner below the header. Two variants:

- `.page-hero` — dark background (`--ink`), cream text. Used for Blog index.
- `.page-hero--indigo` — indigo background (`--indigo`), cream text. Used for Work index.
- `.page-hero--saffron` — saffron background (`--saffron`). Available for future use.

H1 in Playfair Display 900, `clamp(2.5rem, 6vw, 4rem)`. Subtitle in Lora italic, `1.125rem`, `--muted`.

```html
<header class="page-hero page-hero--indigo">
    <div class="container-wide">
        <h1>Work</h1>
        <p>Python scripts, power systems analysis, and network visualizations.</p>
    </div>
</header>
```

### Post Cards

Used in index pages (pidx.html, widx.html) and the home page recent strips.

- `.post-card` — cream background, `3px solid --saffron` left border, subtle box-shadow.
- `.work-card` — same as `.post-card` (can be styled differently in future if needed).
- On hover: border thickens to `5px`, subtle `translateX(2px)` translation.

```html
<article class="post-card">
    <div class="post-meta">
        <span class="post-tag">Art History</span>
        <time class="post-date" datetime="2020-07-28">2020-07-28</time>
    </div>
    <h2><a href="sindh.html">The Land of Two Rivers</a></h2>
    <p class="post-subtitle">A short description of the post.</p>
</article>
```

**Category tags used:**

| Tag | Pages |
|-----|-------|
| `Art History` | sindh.html, indianpaint.html |
| `Reading` | books.html, dauntingproj.html |
| `Meta` | practice.html |
| `Python` | psse-prelim.html, rawfile.html, consumer_con.html |
| `Visualization` | consumer.html, contree.html, netviz.html, flow_alt.html |
| `Power Systems` | magsat.html, roeper-example.html, lineconst.html |

### Code Blocks

Dark panel contrasting strongly with the cream page.

```css
background: var(--code-bg)    /* #1A1814 */
color: var(--code-text)        /* #E8E0D0 */
border-left: 4px solid var(--saffron)
font-family: 'JetBrains Mono', monospace
font-size: 0.875rem
```

Class: `.code-block` (or `<code class="prettyprint">` — overridden by psse.css).

### Data Card

The identity info block on the home and about pages. Same dark panel treatment as code blocks, but inline-block and with wider padding. Class: `.data-card`.

```html
<div class="data-card">
    name    : Amitava Maity<br>
    email   : amaity at rediffmail.com<br>
    twitter : @avamaity<br>
    level   : novice<br>
    work    : power system analyst
</div>
```

### Article Headers

Used at the top of all content pages (within `#main` in psse.css pages, or directly in prose pages).

```html
<div class="article-header">
    <span class="article-tag">Python</span>
    <time class="article-date" datetime="2017-01-08">2017-01-08</time>
    <h1 class="article-title">PSSE — Getting Started</h1>
    <p class="article-subtitle">Brief description of the article.</p>
</div>
```

The `.article-title` gets an `::after` pseudo-element: a `3rem` wide, `3px` tall saffron rule.

### Section Marks (§)

H2 headings in article body get a `§` prefix via CSS `::before`:

```css
#main h2::before,
.content h2::before {
    content: '§ ';
    color: var(--saffron);
}
```

This gives a scholarly texture to essay sections without images or icons.

### Book List Status Classes

Used in `books.html` and `dauntingproj.html`:

```html
<span class="book-read">(PB, Jan 2021)</span>      <!-- green — read -->
<span class="book-reading">[reading]</span>          <!-- indigo — in progress -->
<span class="book-unfinished">[unfinished]</span>    <!-- sienna — abandoned -->
```

### Footer

Dark (`--ink`) background footer on all pages. Barlow Condensed, `0.875rem`.

```html
<footer class="site-footer">
    <p>&copy; Amitava Maity &mdash; <a href="index.html">avamaity</a></p>
</footer>
```

psse.css pages use `<div id="footer">` — styled identically.

---

## Page Templates

### Home (index.html)

```
[.site-header]  — ink background, wordmark + nav
[.hero]         — paper-dark background, large Playfair Display name, subtitle, .data-card
[.intro-grid]   — 3 columns: Why Python / Why Books / Why this site
[.recent-strip] — "RECENT WRITING" label + 3 post-cards
[.recent-strip] — "RECENT WORK" label + 3 work-cards
[.site-footer]  — ink background
```

Body gets `id="page-home"` for page-specific CSS overrides.

### About (about.html)

```
[.site-header]         — ink background, wordmark + nav
[.about-hero]          — 2-column grid
  [.about-portrait]    — saffron background, name in huge Playfair italic
  [.about-content]     — paper background, intro paragraph + .data-card
[.about-sections]      — prose: § What I do, § What I read, § What I write, § This site
[.site-footer]         — ink background
```

Body gets `id="page-about"` for page-specific CSS overrides.

### Blog Index (pages/pidx.html)

```
[.site-header]     — ink background, wordmark + nav
[.page-hero]       — ink background, "Writing" heading
[main.container-prose]  — stacked .post-card elements
[.site-footer]     — ink background
```

### Work Index (work/widx.html)

```
[.site-header]              — ink background, wordmark + nav
[.page-hero.page-hero--indigo]  — indigo background, "Work" heading
[main.container-prose]     — stacked .work-card elements
[.site-footer]              — ink background
```

### Article / Content Page (psse.css template)

All pages in `pages/` and `work/` use `psse.css` with legacy `#id` selectors:

```
[#header]    — styled as .site-header (ink background, wordmark)
[#nav]       — styled as .site-nav (inside ink bar)
[#main]      — max-width 680px, centered, generous padding
  [.article-header]  — tag + date + .article-title + .article-subtitle
  [article body content]
[#footer]    — styled as .site-footer (ink background)
```

**Required HTML in `#header`:**
```html
<div id="header">
    <h1><a href="../index.html">avamaity</a></h1>
</div>
```

---

## Implementation Notes

### CSS File Responsibilities

| File | Used by | Purpose |
|------|---------|---------|
| `css/main.css` | index.html, about.html, pages/pidx.html, work/widx.html | Full design system + page-specific components |
| `css/psse.css` | All `pages/*.html` and `work/*.html` content articles | Same design tokens + legacy `#id` selector overrides + article-specific styles |

**Important:** `psse.css` duplicates the design tokens from `main.css` so content pages don't need to import both files. They are kept in sync manually.

### Google Fonts

Both CSS files import the same Google Fonts URL at the top. HTML files also include `<link rel="preconnect">` tags for performance:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

The `@import` in the CSS handles the actual font load.

### HTML Migration Checklist

When updating a legacy content page to the new design:

- [ ] Update DOCTYPE to `<!DOCTYPE html>`
- [ ] Add `<meta charset="utf-8">` and `<meta name="viewport">`
- [ ] Update `<title>` to format: `Page Title — avamaity`
- [ ] Add Google Fonts `<link rel="preconnect">` tags
- [ ] Change CSS link from `psse.css` (already correct for content pages)
- [ ] Remove MathJax script (or keep if page uses math notation)
- [ ] Remove Google Prettify script (psse.css overrides its output)
- [ ] Remove Twitter widget scripts
- [ ] Update `#header`: replace `<h1><img>avamaity</h1>` with `<h1><a href="...">avamaity</a></h1>`
- [ ] Move `#nav` out of `#content` wrapper (remove `#content` div entirely)
- [ ] Add `class="active"` to the correct nav `<li>`
- [ ] Add `.article-header` div at top of `#main` with tag, date, title, subtitle
- [ ] Upgrade heading structure: `<h4><b>Section</b></h4>` → `<h2>Section</h2>`
- [ ] Replace `<font color>` tags with CSS classes (`book-read`, `book-reading`, `book-unfinished`)
- [ ] Fix invalid HTML: `<li>` elements inside `<p>` → proper `<ul>` or `<ol>`
- [ ] Update `#footer`: remove Twitter widget, add `<p>&copy; Amitava Maity &mdash; <a href="../index.html">avamaity</a></p>`

---

## Changelog

| Version | Date | Notes |
|---------|------|-------|
| v2.0 | 2026-04 | Bold "Kolkata Editorial" redesign. New palette (ink/cream/saffron/indigo), Google Fonts (Playfair Display + Barlow Condensed + Lora + JetBrains Mono), full CSS rewrites, post-card components, article-header pattern, dark code panels. |
| v1.0 | 2015–2024 | Minimal system-ui design. Light gray background, blue accent, plain list navigation for indexes. |
