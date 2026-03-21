# Typography System
**Project:** TReDS Bid Position Awareness — Case Study
**Framework:** Vanilla HTML/CSS/JS
**Stack:** Google Fonts · CSS Custom Properties · No Tailwind
**Scale Ratio:** Perfect Fourth · 1.333

---

## Font Stack

```css
:root {
  --font-display: 'Cormorant Garamond', Georgia, 'Times New Roman', serif;
  --font-body:    'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-mono:    'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
}
```

**Google Fonts URL (current `<head>`):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
```

**Why this pairing works:**
Cormorant Garamond is a high-contrast, optically-sized display serif — it gains character as it gets larger. Inter is designed specifically for screen legibility at 12–18px. The contrast between editorial serif and functional sans mirrors the case study's own tension: elegant surface, rigorous analysis underneath.

**Variable font status:** Not using variable axes — static weights load faster for a portfolio site.
**Weights loaded:** Cormorant 300/400/500 (regular + italic); Inter 300/400/500/600.

---

## Type Scale

**Ratio:** Perfect Fourth (×1.333) · Base 16px · Viewport 375px → 1280px

```css
:root {
  /* ─── Fluid Type Scale ─── */
  --text-xs:   clamp(0.688rem, 0.22vw + 0.636rem, 0.813rem);  /* 11px → 13px  */
  --text-sm:   clamp(0.813rem, 0.22vw + 0.761rem, 0.938rem);  /* 13px → 15px  */
  --text-base: clamp(1rem,     0.22vw + 0.948rem, 1.125rem);  /* 16px → 18px  */
  --text-lg:   clamp(1.125rem, 0.44vw + 1.021rem, 1.375rem);  /* 18px → 22px  */
  --text-xl:   clamp(1.375rem, 0.77vw + 1.194rem, 1.813rem);  /* 22px → 29px  */
  --text-2xl:  clamp(1.813rem, 1vw    + 1.578rem, 2.375rem);  /* 29px → 38px  */
  --text-3xl:  clamp(2rem,     2.24vw + 1.25rem,  3.125rem);  /* 32px → 50px  ← hero display */
  --text-4xl:  clamp(3.188rem, 1.88vw + 2.748rem, 4.25rem);   /* 51px → 68px  */
  --text-5xl:  clamp(4.25rem,  2.43vw + 3.68rem,  5.625rem);  /* 68px → 90px  */

  /* ─── Matched Line Heights ─── */
  --leading-xs:   1.55;
  --leading-sm:   1.55;
  --leading-base: 1.75;   /* paragraph text */
  --leading-lg:   1.65;   /* large body / intro */
  --leading-xl:   1.45;
  --leading-2xl:  1.30;
  --leading-3xl:  1.10;   /* hero display — tight for serif */
  --leading-4xl:  1.05;
  --leading-5xl:  1.0;

  /* ─── Letter Spacing ─── */
  --tracking-xs:   0.02em;   /* open — small labels */
  --tracking-sm:   0.01em;
  --tracking-base: 0em;
  --tracking-lg:   0em;
  --tracking-xl:  -0.01em;
  --tracking-2xl: -0.01em;
  --tracking-3xl: -0.015em;  /* hero display */
  --tracking-4xl: -0.02em;
  --tracking-5xl: -0.025em;

  /* ALL CAPS overline/label rule: always +0.08em to +0.18em regardless of size */

  /* ─── Font Weights ─── */
  --weight-light:    300;
  --weight-normal:   400;
  --weight-medium:   500;
  --weight-semibold: 600;
}
```

**Usage mapping:**

| Token        | Size range     | Line-height | Use in this project               |
|--------------|----------------|-------------|-----------------------------------|
| `--text-xs`  | 11px → 13px    | 1.55        | Badges, sub-labels, captions      |
| `--text-sm`  | 13px → 15px    | 1.55        | Platform UI cells, FTU sub-labels |
| `--text-base`| 16px → 18px    | 1.75        | Body paragraphs (`.body`)         |
| `--text-lg`  | 18px → 22px    | 1.65        | Large body, intro text            |
| `--text-xl`  | 22px → 29px    | 1.45        | Pull quotes, callout statements   |
| `--text-2xl` | 29px → 38px    | 1.30        | Section subheads                  |
| `--text-3xl` | 32px → 50px    | 1.10        | **Hero copy** (`.hc-big`)         |
| `--text-4xl` | 51px → 68px    | 1.05        | Large display (unused currently)  |
| `--text-5xl` | 68px → 90px    | 1.0         | Decorative display (unused)       |

---

## Vertical Rhythm

**Baseline unit:** `1rem × 1.75` (body text line-height) = 28px
**Grid unit:** 8px (the visual grid the platform mockup uses — consistent with Inter's default metrics)

```css
:root {
  --rhythm-unit:   1.75rem;   /* 28px — matches body leading */
  --rhythm-half:   0.875rem;  /* 14px — tight spacing        */
  --rhythm-double: 3.5rem;    /* 56px — section breathing    */
  --rhythm-triple: 5.25rem;   /* 84px — slide-level padding  */
  --prose-max-width: 62ch;    /* optimal for Inter at --text-base */
}
```

**Spacing guide for this project:**
- Overline `.lbl` → headline: `28px` (--rhythm-unit)
- Hero headline → body lines: `16px` (slightly under half-rhythm — display serifs need tighter pull)
- Body copy `p` → `p`: `12px` (current implementation ✓)
- `.byline` margin-top: `44px` ≈ `--rhythm-double` (correct ✓)
- Slide padding: `56px 80px 96px` — bottom is generous for nav overlap (correct ✓)

---

## Font Loading

**Current implementation (vanilla HTML):**
```html
<!-- In <head> — already correct. preconnect reduces DNS lookup time -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
```

**`display=swap` is set** — text renders in fallback font immediately, swaps when fonts load. For a case study portfolio this is the right choice (content-first).

**Fallback stacks** (already in `:root`):
- `--font-display` fallback: `Georgia` — similar x-height ratio to Cormorant, prevents jarring layout shift
- `--font-body` fallback: `-apple-system` — matches Inter's metrics on macOS/iOS

**Performance note:** 6 font files total (3 Cormorant weights × 2 styles + 4 Inter weights, but only unicode ranges used per page load). For a single-page case study this is acceptable.

---

## Accessibility

- **Minimum body text:** `--text-base` = 16px ✓ (all body copy uses 15–16px minimum)
- **Minimum caption:** `--text-xs` = 11px → used only for platform mockup UI cells (acceptable in context — it's a mockup, not content)
- **Optimal line length:** `--prose-max-width: 62ch` — `.body` currently uses `max-width:460px` ≈ 55–60ch at base size ✓
- **Color contrast:** `var(--t)` = `#f0ebe4` on `var(--bg)` = `#0a0a0a` → contrast ratio ≈ **18.6:1** (AAA ✓)
- **`var(--t2)`** = `rgba(240,235,228,0.62)` on `#0a0a0a` → effective `#a09a93` → contrast ≈ **9.8:1** (AA ✓)
- **`var(--t3)`** = `rgba(240,235,228,0.30)` on `#0a0a0a` → ≈ **4.1:1** — borderline AA. Used only for decorative labels (overlines, bylines) — acceptable
- **Line height body:** `1.75` — above the WCAG 1.5 minimum ✓
- **Italic usage:** Cormorant Garamond italic is used for display text only — body copy remains upright Inter ✓
- **Reduced motion:** Slide transitions use `transform` — no text animations that would need `prefers-reduced-motion` exceptions

---

## Hero Slide (Slide 01) — Applied Scale

The hero copy uses these tokens in practice:

```css
/* Hero display line — ₹8.97 Cr lost — in a single auction */
.hc-big {
  font-family: var(--font-display);   /* Cormorant Garamond */
  font-style:  italic;
  font-weight: var(--weight-normal);  /* 400 */
  font-size:   clamp(32px, 3.6vw, 50px);  /* ≈ --text-3xl */
  line-height: var(--leading-3xl);    /* 1.10 */
  letter-spacing: var(--tracking-3xl); /* -0.015em */
}

/* Statement lines — 4× single-line statements */
.hc-lines {
  font-family: var(--font-body);      /* Inter */
  font-size:   clamp(15px, 1.6vw, 19px);  /* between --text-sm and --text-lg */
  line-height: var(--leading-lg);     /* 1.65 — statements, not paragraphs */
}

/* Bold final line — They lost every bid */
.hc-lines strong {
  font-weight:     var(--weight-semibold);  /* 600 */
  letter-spacing:  -0.01em;               /* slight tightening at this weight */
}
```

**Why these decisions:**
- Cormorant at `clamp(32px → 50px)` enters its optical sweet spot — the high-contrast strokes become readable and elegant simultaneously
- `-0.015em` tracking on italic display text pulls the letterforms together, preventing the slight looseness that italic angle introduces at large sizes
- `line-height: 1.10` is tight but Cormorant italic at this size has minimal descenders — the ascenders create the vertical rhythm
- Statement lines at `1.65` — tighter than paragraph `1.75` because each line is a complete thought, not part of a flowing read
- The weight contrast: display in 400 italic vs statements in 400 → strong in 600 is the correct 3-stop hierarchy without using size alone

---

## Notes for `generate-theme`

- **Font families are decided** — skip font selection in generate-theme, use `--font-display` and `--font-body` tokens above
- Scale tokens (`--text-*`) are defined here — generate-theme should include them as constant tokens
- The dark case study theme (`--bg: #0a0a0a`) and light platform theme (white) are already established — themes should extend these, not replace them
