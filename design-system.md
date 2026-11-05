# MediaMister Panel — Design System

Extracted from the compiled CSS of https://panel.mediamister.com/ (`/assets/index-BTJVPAuV.css`). Light theme only (no `prefers-color-scheme` rules found).

## Tokens (CSS custom properties)

```css
:root {
  /* Brand */
  --color-primary: #3740ff;
  --color-primary-hover: #2a33e0;
  --color-primary-active: #232bd0;
  --color-primary-soft: #eef0ff;
  --color-primary-soft-strong: #e3e6ff;
  --color-primary-border: #c7cbff;
  --color-primary-ring: #3740ff4d;
  --brand-bright: #5f66ff;
  --color-navy: #0b2545;   /* = --color-ink, headings / strong text */
  --navy-soft: #12345c;

  /* Neutrals */
  --color-page-bg: #f5f7fa;
  --color-surface: #fff;
  --color-surface-muted: #f9fafb;
  --color-surface-subtle: #f3f4f6;
  --color-border: #e5e7eb;
  --color-border-strong: #d1d5db;
  --color-text-secondary: #6b7280; /* = --color-text-muted */

  /* Status */
  --color-success: #16a34a; --color-success-soft: #ecfdf3; --color-success-border: #bbf7d0; --color-success-text: #166534;
  --color-warning: #d97706; --color-warning-soft: #fffbeb; --color-warning-border: #fde68a; --color-warning-text: #92400e;
  --color-danger:  #dc2626; --color-danger-soft:  #fef2f2; --color-danger-border:  #fecaca; --color-danger-text:  #b91c1c; --color-danger-hover: #b91c1c;

  /* Type */
  --font-sans: system-ui, "Segoe UI", Roboto, sans-serif;
  --font-size-xs: .75rem;     /* 12px */
  --font-size-sm: .8125rem;   /* 13px */
  --font-size-base: .875rem;  /* 14px */
  --font-size-md: .95rem;
  --font-size-lg: 1.125rem;   /* 18px */
  --font-weight-medium: 500; --font-weight-semibold: 600; --font-weight-bold: 700;

  /* Spacing (4px scale; no space-7 / space-9) */
  --space-1: 4px; --space-2: 8px; --space-3: 12px; --space-4: 16px;
  --space-5: 20px; --space-6: 24px; --space-8: 32px; --space-10: 40px;
  --dashboard-page-gutter: 14px;

  /* Radius */
  --radius-sm: 8px; --radius-md: 10px; --radius-lg: 12px; --radius-pill: 999px;

  /* Elevation (navy-tinted shadows) */
  --shadow-xs: 0 1px 2px #0b25450d;
  --shadow-sm: 0 1px 3px #0b254514, 0 1px 2px #0b25450a;
  --shadow-md: 0 4px 12px #0b254514;
  --shadow-lg: 0 12px 32px #0b254524;

  /* Interaction */
  --focus-ring: 0 0 0 3px var(--color-primary-ring);
  --btn-ease: cubic-bezier(.22, 1, .36, 1);
}
```

Semantic aliases used in the app: `--bg`=page-bg, `--card`=surface, `--line`=border, `--ink`/`--navy`=navy, `--muted`=text-secondary, `--brand`=primary.

## Components (`.ds-*` classes)

| Component | Notes |
|---|---|
| `.ds-btn` | 40px high, 0 16px padding, radius-sm, 14px / 600, 1px transparent border, inline-flex gap 8px; transitions .18s. Variants: `--primary`, `--secondary` (soft brand hover), `--neutral`, `--ghost`, `--danger`, `--danger-solid`; sizes `--sm`, `--lg`; `--block`, `--loading` (spinner via `:after`). Per-variant `--btn-glow` RGB: blue 37,99,235; green 5,150,105; amber 245,158,11; red 220,38,38. |
| `.ds-card` | surface bg, 1px border, radius-lg (12px), no shadow. Parts: `__header`, `__title`, `__body`, `__footer`, `--padded`. |
| `.ds-badge` | 12px / 600, padding 3px 9px, radius-sm, bordered. Variants: `--brand`, `--success`, `--warning`, `--danger`. |
| `.ds-alert` | Variants `--info`, `--success`, `--warning`, `--danger`; `__icon`. |
| Forms | `.ds-field`, `.ds-label`, `.ds-help`, `.ds-error-text`, `.ds-input`, `.ds-select`, `.ds-textarea` (+ `--error`: red border, 3px `#dc262633` ring), `.ds-check`, `.ds-radio`, `.ds-switch`. Focus = `--focus-ring`. |
| Table | `.ds-table-wrap`, `.ds-table`; pagination `.ds-pagination`, `.ds-page-btn(--active)`. |
| Navigation | `.ds-tabs`, `.ds-tab(--active)`, `.ds-dropdown`, `.ds-dropdown__item(--active)`. |
| Overlay | `.ds-modal-backdrop`, `.ds-modal` (`__header/__title/__subtitle/__body/__footer`), `.ds-tooltip`. |
| Misc | `.ds-stat` (`__icon/__body/__label/__value/__meta`), `.ds-empty` (`__icon/__title/__text`), `.ds-skeleton`. |

## Principles observed
- Calm, flat SaaS look: white cards on `#f5f7fa`, hairline borders, almost no shadow on cards; shadows reserved for popovers/modals.
- One accent (indigo `#3740ff`) plus deep navy for text; status colors come as solid / soft / border / text quartets.
- Compact density: 14px base text, 40px controls, 8px radius on controls and 12px on containers.
- Responsive tables collapse to stacked rows on mobile (`dashboard-table--mobile-stack`).

---

# Landing page — `index.html` (current state)

Single static page, light theme with navy/blue accent sections. Everything below is implemented in the inline `<style>` of `index.html`; it reuses the tokens above and adds a type scale and a few layout/motion conventions. Assets: `assets/logo.svg` (header), `assets/text-logo.svg` (footer wordmark), `assets/stack-bg.svg` (blue gradient used on the "One Panel" card).

## Added tokens

```css
/* "MM Fluid Scale" — fluid type */
--fs-display: clamp(2.375rem, 1.5rem + 4.2vw, 4.5rem);   /* hero H1 */
--fs-title:   clamp(1.75rem, 1.3rem + 2vw, 2.75rem);      /* sub-headings / big stat text */
--fs-section: clamp(2.25rem, 1.2rem + 2.63vw, 3.5rem);    /* every section H2 */
--fs-heading: clamp(1.125rem, 1.05rem + .5vw, 1.5rem);    /* card / H3 */
--fs-lead:    clamp(1rem, .95rem + .3vw, 1.1875rem);
--fs-body: .9375rem;  --fs-small: .875rem;  --fs-caption: .75rem;
--lh-tight: 1.08; --lh-snug: 1.45; --lh-body: 1.65;
--ls-display: -.035em; --ls-title: -.025em; --ls-caps: .08em;
```

Other fixed colors used on the page: stack blue `#1b2a8c` (+ `stack-bg.svg`), pastel tints `--base/--g1…g5` per tile class (`.t-aurora`, `.t-sky`, `.t-lav`, `.t-rose`, `.t-mint`, `.t-peach`, `.t-navy`), card sky `#d6e6ff`.

## Page structure (top → bottom)

| Section (`id`) | Background | Notes |
|---|---|---|
| Header | page bg | Logo + API / MCP anchors + Log In (secondary btn). **Mobile ≤600px:** plain three-line hamburger (no background, 24px lines, turns into ×) opening a white rounded dropdown with API, MCP and a full-width Log In; closes on link tap, outside tap, Esc or widening past 600px |
| Hero | page bg + grid + glow | H1 "Media Mister *SMM Panel*", Create Your Account (primary) / Log In (secondary), tile row with aurora + grain |
| One Panel (`about`) | white | Centered headline; blue stack stage `#1b2a8c` with swapping cards (auto swap ≈1.9 s); "Since 2012" block. Line divider above has no circle |
| Services (`services`) | white | Centered intro, primary CTA, 6 platform cards (single blue theme, glass geometric shape + grain) |
| Why choose (`why`) | white | Scroll-velocity headline + scrolling card row; white cards, pricing-style shadow, blue two-tone icons |
| How to use (`how`) | grid-line white | Pinned, scroll-driven 5 steps + device mockup (white, 36px radius, translucent frame ring). **Mobile ≤900px:** not pinned, mockup (≈280px) sticky above the steps and stops where the list ends; CTA after last step |
| Pricing (`pricing`) | white | "To-do" card: blue stack-bg header (example package pills), white checklist panel with selecting-dot animation (9 s loop, all clear together) |
| Rewards (`rewards`) | white + fading grid lines | Swapping membership cards (Basic green / Bronze / Silver / Gold / Diamond / Platinum) each with its own pattern, coloured shadow, shine sweep; two plain info boxes (rows stack on mobile) |
| Track orders (`track-orders`) | page bg | Status table with coloured pills (stacks to cards on ≤600px); Refill & Money-Back block with divider line, vertical lines, numbered 01/02 items |
| Account + API (`account`, `api`) | white | 2×2 bordered text grid; API checklist box; navy CTA |
| MCP (`mcp`) | page bg | Animated AI input box (types the 3 example prompts one by one), counting stat tiles (5 / 100), client pills |
| Ways of working (`ways`) + Referrals | white | Newspaper-style 4-column text (vertical rules, icon + big bold name); language pills with SVG flags (single row desktop, wraps to 2 rows ≤700px); referrals segmented progress bar (gradient segments fill in sequence) |
| FAQ (`faq`) | page bg + fading vertical lines | Headline above; sticky left line + 16-item accordion (`<details name="faq">`, plus icon 36px) |
| Closing CTA (`start`) | white; blue stack-bg banner | White icon pattern revealed near the cursor (not over text/buttons), primary white + outlined secondary buttons |
| Footer | flat `#0b2545` + faint white vertical lines | Tagline, X / YouTube / TikTok 44px outlined circle icon buttons (placeholder `#` links; white fill + lift on hover), three link columns, copyright + Back to top (no divider line above it), faded full-width wordmark (`text-logo.svg`, not hoverable) |

## Components & patterns

- **Buttons** (`.btn`): pill, 48px (58px in hero/sections), `.btn-primary` = navy `#0b2545` → blue on hover, no shadow at rest; `.btn-secondary` = white with strong border. Hover scales 1.07. **Mobile ≤600px:** every button is scaled to 80% via `zoom: .8` (height, padding, text, icon); **≤480px** buttons are `width: 80%` and centered instead of full width. Exceptions: nav Log In inside the hamburger menu is full width at 46px; the pricing-card button is auto width, single line, with fluid side padding (`clamp(18px, 5.5vw, 44px)`).
- **Glass/tint cards** (`.fcard`): white background, hairline ring + `0 8px 18px #0b25451a` shadow (shared with the pricing card); hover lifts and deepens shadow.
- **Pills**: status pills (`.st-*`: amber / blue / green / orange / red, medium weight), language pills (flag in 24px rounded square), client pills, example-package pills.
- **Icons**: two-tone blue outline set (outline `#232bd0`, fills `#c7cbff` / `#6f76ff`, 3px stroke, rounded joins) at 56–60px.
- **Grain**: SVG `feTurbulence` overlay, `mix-blend-mode: overlay`, used on tiles, banner, footer glow, services cards.
- **Lines**: `repeating-linear-gradient(90deg, #0b25450d 0 1px, transparent 1px 104px)` on Refill, FAQ (navy-on-light) and footer (white `#ffffff12`).
- **Reveal**: `[data-reveal]` → `.rv` / `.rv-in` (slide-up + blur); not applied to sticky elements.
- **Anchors**: global smooth-scroll handler (own rAF animation, pauses the pinned-steps logic) for every `a[href^="#"]` whose target exists.
- **Reduced motion**: every animation above has a `prefers-reduced-motion` fallback (static final state).

## Responsive rules

| Breakpoint | Changes |
|---|---|
| ≤1000px | Why cards 2-up; Ways grid 2×2 |
| ≤900px | How-to section un-pinned (see above); FAQ and Refill columns stack, sticky off |
| ≤800px | Two-column cards (tracking guarantees, pricing grid) stack |
| ≤700px | Language pills wrap (2 rows) and shrink, flags 18px, no horizontal scroll |
| ≤600px | Header → hamburger; all buttons 80%; status table → stacked rows (pill above meaning, no horizontal scroll); rewards info rows stack label/value; Ways grid single column |
| ≤480px | Buttons 80% width (centered); pricing-card button stays single line |

## Open items
- Placeholder links: `#refund-policy`, `#api-docs`, `#mcp-setup`, `#signup`, `#login`, footer social icons (`#`).
- No newsletter signup in the footer.
