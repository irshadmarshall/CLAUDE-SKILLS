# Brand Guidelines v1.0

> Last updated: 2026-07-12
> Status: Draft — compiled from the Diet Pro menu deck (45pp, Jul 2026)

## Quick Reference

| Element | Value |
|---------|-------|
| Primary Color | #1C3C2E |
| Secondary Color | #E2953A |
| Accent Color | #6EA83A |
| Primary Font | Baloo 2 |
| Voice | Matter-of-fact, Warm, Precise |

---

## 1. Color Palette

### Primary Colors

| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Forest Green | #1C3C2E | rgb(28,60,46) | Primary ground, "diet" wordmark, category labels, featured subscription card |
| Forest Green Dark | #12271D | rgb(18,39,29) | Hover / shadow states on Forest |

### Secondary Colors

| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Amber | #E2953A | rgb(226,149,58) | Prices, the "pro." signature, tagline emphasis, CTAs |
| Amber Dark | #C97B22 | rgb(201,123,34) | Hover states, emphasis |

### Accent Colors

| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Vegan Green | #6EA83A | rgb(110,168,58) | Positive/success states, "Vegan" nutrition tag |
| Vegan Green Light | #A7CD68 | rgb(167,205,104) | "Vegetarian" nutrition tag |

### Neutral Palette

| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Background | #FAF1E1 | rgb(250,241,225) | Menu & document paper ground — never pure white |
| Surface | #FFFAF0 | rgb(255,250,240) | Cards, menu tiles |
| Text Primary | #26231D | rgb(38,35,29) | Body copy — warm near-black, never pure #000 |
| Text Secondary | #6C6255 | rgb(108,98,85) | Captions, muted text |
| Border | rgba(38,35,29,0.14) | — | Dividers, borders |

### Nutrition Tag Palette (fixed, non-brand)

| Name | Hex | Usage |
|------|-----|-------|
| High-Protein | #E2953A | Protein claim — shares the brand accent since it's the hero claim |
| High-Fibre | #234A37 | Fibre claim |
| Weight Loss | #E2695A | Weight-loss claim |
| Gluten-Free | #E4BA3D | Gluten-free claim |
| Keto | #8A5D33 | Keto claim |
| Stat Tile Ground | #E9F0DF | Macro stat tiles (kcal / protein / carbs / fat / fibre) |

### Accessibility

- Text (Ink #26231D) on Cream (#FAF1E1): 12.9:1 contrast ratio (AAA)
- Cream text on Forest Green: 9.7:1 contrast ratio (AAA)
- Amber on Forest Green: 4.6:1 contrast ratio (AA) — large/bold use only (prices, signature), not body copy
- All interactive elements meet WCAG 2.1 AA

---

## 2. Typography

### Font Stack

```css
--font-heading: 'Baloo 2', 'Arial Black', sans-serif;
--font-body: 'Poppins', 'Segoe UI', sans-serif;
--font-mono: ui-monospace, monospace;
```

### Type Scale

| Element | Font | Weight | Size (Desktop/Mobile) | Line Height |
|---------|------|--------|----------------------|-------------|
| H1 / Cover tagline | Baloo 2 | 800 | 44px / 32px | 1.1 |
| H2 / Section head | Baloo 2 | 800 | 32px / 26px | 1.2 |
| H3 / Category eyebrow | Baloo 2 | 700 | 18px / 16px | 1.3 |
| Signature script | Caveat | 700 | signature use only | 1.0 |
| Price | Poppins | 700 | 15px / 15px | 1.4 |
| Body | Poppins | 400 | 16px / 16px | 1.6 |
| Caption / Stat label | Poppins | 500 | 12px / 12px | 1.4 |

### Font Loading

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@600;700;800&family=Poppins:wght@400;500;600;700&family=Caveat:wght@600;700&display=swap" rel="stylesheet">
```

---

## 3. Logo Usage

### Variants

| Variant | File | Use Case |
|---------|------|----------|
| Primary lockup (Cream on Forest) | logo-primary.svg | Headers, menu covers, dark applications |
| Reversed lockup (Forest on Cream) | logo-reversed.svg | Menu cards, documents, light applications |
| Arabic companion (دايت برو) | logo-ar.svg | UAE-market bilingual materials |

### Clear Space

Minimum clear space = cap-height of "diet"

### Minimum Size

| Context | Minimum Width |
|---------|---------------|
| Digital — Full Logo | 120px |
| Print — Full Logo | 35mm |

### Don'ts

- Don't recolor "pro." to anything outside Amber
- Don't add shadows, outlines, or gradients to the wordmark
- Don't stretch, rotate, or reset the baseline shift between "diet" and "pro."
- Don't place the mark over a busy food photograph without a solid safe zone

---

## 4. Voice & Tone

### Brand Personality

| Trait | Description |
|-------|-------------|
| **Matter-of-fact** | States what's in the dish and what it does — never "revolutionary fuel" |
| **Warm, not clinical** | Pleasure is allowed alongside protein counts — "tastes like dessert" |
| **Precise** | Exact grams, allergens, and serving sizes — never a vague claim when a number is available |
| **Unbothered** | No countdowns, no diet-culture urgency — eating well is routine, not an event |

### Voice Chart

| Trait | We Are | We Are Not |
|-------|--------|------------|
| Matter-of-fact | Numeric, evidence-first | Hype-driven, "miracle" language |
| Warm | Sensory, food-loving | Clinical, spreadsheet-cold |
| Precise | Exact grams and allergens | Vague ("a good source of") |
| Unbothered | Routine, everyday | Urgent, countdown-driven |

### Tone by Context

| Context | Tone | Example |
|---------|------|---------|
| Menu description | Sensory, specific | "Aji amarillo-marinated lean chicken breast grilled to perfection, served over silky sweet-potato mash." |
| Nutrition claim | Plain, numeric | "Zero refined sugar, 12g protein." |
| Allergens / legal | Flat, unambiguous | "Fish (salmon), soy (ponzu contains soy sauce), sesame." |
| Subscription / app | Direct, benefit-first | "Pause or skip anytime. Free UAE-wide delivery." |
| Marketing / tagline | Terse, confident | "Eat smart. Live sharp." |

### Prohibited Terms

| Avoid | Reason |
|-------|--------|
| Detox miracle | Unsubstantiated medical claim |
| Clean eating | Moralizing, diet-culture language |
| Cheat day | Frames food as good/bad |
| Guilt-free (as a marketing claim) | Reserved only as the fixed category name "Guilt-Free Desserts" |
| Countdown / urgency copy | Contradicts the "unbothered" trait |

---

## 5. Imagery Guidelines

### Photography Style

- **Lighting:** Soft, directional daylight — no harsh flash
- **Subjects:** Real plates as served — speckled stoneware, linen napkin, brass or wood accents
- **Color treatment:** True-to-ingredient color, no over-saturation or filter grading
- **Composition:** 3/4 or top-down angle, generous negative space for text overlay

### Illustrations

- Style: None — the brand relies on photography, not illustration
- Colors: Brand palette only, if ever used
- Stroke: 2px consistent, if ever used

### Icons

- Style: Outlined, 24px base grid
- Corner radius: 4px

---

## 6. Design Components

### Buttons

| Type | Background | Text | Border Radius |
|------|------------|------|----------------|
| Primary | #E2953A | #FFFFFF | 9999px (pill) |
| Secondary | Transparent, 1px Forest border | #1C3C2E | 9999px (pill) |

### Spacing Scale

| Token | Value | Usage |
|-------|-------|-------|
| xs | 4px | Tight spacing |
| sm | 8px | Compact elements |
| md | 16px | Standard spacing |
| lg | 24px | Section spacing |
| xl | 32px | Large gaps |
| 2xl | 48px | Section dividers |

### Border Radius

| Element | Radius |
|---------|--------|
| Menu cards | 18px |
| Stat tiles | 10px |
| Tags / pills | 9999px |
| Buttons | 9999px |

---

## AI Image Generation

### Base Prompt Template

```
Overhead or 3/4 angle food photography, natural daylight, speckled stoneware bowl, warm linen napkin, true-to-ingredient color, no over-saturation, shallow depth of field, Diet Pro healthy-food brand
```

### Style Keywords

| Category | Keywords |
|----------|----------|
| **Lighting** | soft daylight, directional, no flash |
| **Mood** | wholesome, unfussy, confident |
| **Composition** | 3/4 angle, top-down, generous negative space |
| **Treatment** | true color, natural, unfiltered |
| **Aesthetic** | real plates, rustic stoneware, minimal styling |

### Visual Mood Descriptors

- Real food as actually served, not styled beyond recognition
- Warm and appetizing without looking "produced"
- Confident, protein-forward, never clinical

### Visual Don'ts

| Avoid | Reason |
|-------|--------|
| Over-saturated color grading | Reads as filtered stock photography |
| Studio-white seamless backdrops | Contradicts the warm, homely tone |
| Stock "lifestyle" people shots | The food is the subject, not a lifestyle scene |

### Example Prompts

**Hero Banner:**
```
Wide shot of a speckled stoneware bowl with sushi-grade salmon poke over rice, edamame, avocado, natural daylight from the left, warm linen surface, Diet Pro brand food photography
```

**Social Media Post:**
```
Top-down shot of a protein pancake stack with berries and sugar-free syrup on a cream ceramic plate, soft daylight, minimal styling, square crop
```

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-07-12 | Initial guidelines, compiled from the Diet Pro menu deck (45pp, Jul 2026) |
