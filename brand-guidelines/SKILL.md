---
name: brand-guidelines
description: Use this skill when styling components, creating new pages, or ensuring visual consistency across the Ential website. Contains fonts, colors, and design patterns.
allowed-tools: Read, Edit, Write, Glob, Grep
---

# Brand Guidelines

This skill defines the visual identity for the Ential website, ensuring consistency across all components and pages.

## Typography

### Font Families

| Font | Usage | CSS Variable | Tailwind Class |
|------|-------|--------------|----------------|
| **Instrument Serif** | Headings, titles, hero text, all major headings | `font-family: 'Instrument Serif', serif` | `font-display` or `font-serif` |
| **JetBrains Mono** | Body text, UI elements, code, labels | `font-family: 'JetBrains Mono', monospace` | `font-mono` |
| **Space Grotesk** | Stats, numbers, emphasis, card titles | `font-family: 'Space Grotesk', sans-serif` | `font-sans` |

### Font Import (Required)

```css
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&display=swap');
```

### Heading Hierarchy

| Element | Style | Example Usage |
|---------|-------|---------------|
| `h1` (Hero) | Instrument Serif, `text-5xl sm:text-6xl md:text-7xl lg:text-8xl` | Page titles, hero sections |
| `h2` (Section) | Instrument Serif, `text-4xl md:text-5xl lg:text-6xl` | Section headings |
| `h3` (Subsection) | Instrument Serif or Sans, `text-2xl` or `text-xl` | Subsection headings, card titles |
| Body | JetBrains Mono or default | Paragraphs, UI text |

### Gradient Text Pattern

All major headings should use gradient text for accent words:

```tsx
<h1 className="font-display text-5xl md:text-7xl">
  Main Text{' '}
  <span className="gradient-text italic">Accent Word</span>
</h1>
```

```css
.gradient-text {
  background: linear-gradient(135deg, #f59e0b 0%, #fbbf24 50%, #f59e0b 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

**Blog Post h2 Rule:** All h2 headings in blog posts MUST use amber color:
```tsx
<h2 className="text-amber-500 font-serif text-2xl">Section Title</h2>
```

## Color Palette

### Core Colors

| Name | Hex | Usage | Tailwind |
|------|-----|-------|----------|
| **Black** | `#0a0a0a` | Primary dark background | `bg-[#0a0a0a]` |
| **Very Dark** | `#030303` | Very dark backgrounds | `bg-[#030303]` |
| **Cream** | `#faf8f3` | Light mode background | `bg-[#faf8f3]` |
| **Ink** | `#1a1a1a` | Light mode text, dark mode background | `bg-[#1a1a1a]` |
| **Off-White** | `#e8e6e1` | Dark mode text | `text-[#e8e6e1]` |

### Accent Colors (Amber Scale)

| Shade | Hex | Tailwind Class | Usage |
|-------|-----|----------------|-------|
| Amber 400 | `#fbbf24` | `text-amber-400`, `bg-amber-400` | Hover states, button hover |
| **Amber 500** | `#f59e0b` | `text-amber-500`, `bg-amber-500` | Primary accent, links, headings, buttons |
| Amber 600 | `#d97706` | `text-amber-600`, `bg-amber-600` | Active states, gradients |

### Text Colors (Dark Mode)

| Use Case | Class | Opacity |
|----------|-------|---------|
| Primary text | `text-white` | 100% |
| Secondary text | `text-white/60` | 60% |
| Muted text | `text-white/40` or `text-white/50` | 40-50% |
| Accent text | `text-amber-500` | 100% |

### Background Colors (Dark Mode)

| Use Case | Class | Opacity |
|----------|-------|---------|
| Primary background | `bg-[#0a0a0a]` | Solid |
| Very dark background | `bg-[#030303]` | Solid |
| Card background (subtle) | `bg-white/[0.02]` | 2% |
| Card background (medium) | `bg-white/[0.03]` | 3% |
| Card background (stronger) | `bg-white/[0.05]` | 5% |

### Border Colors

| Use Case | Class | Opacity |
|----------|-------|---------|
| Subtle border | `border-white/10` | 10% |
| Medium border | `border-amber-500/20` | 20% |
| Strong border | `border-amber-500/30` | 30% |
| Strongest border | `border-amber-500/40` | 40% |
| Solid border | `border-amber-500` | 100% |

### CSS Variables

```css
/* Light Mode */
:root {
  --cream: #faf8f3;
  --ink: #1a1a1a;
  --accent: rgb(245, 158, 11);  /* amber-500 */
}

/* Night Mode */
:root.night-mode {
  --cream: #1a1a1a;
  --ink: #e8e6e1;
  --accent: rgb(245, 158, 11);  /* amber-500 stays same */
}
```

## Button System

### Primary Button (Standard Pattern)

**CRITICAL RULE:** Primary buttons use `text-black` on amber background (NOT white text).

```tsx
<a
  href={url}
  className="group inline-flex items-center justify-center gap-3 font-bold bg-amber-500 text-black transition-all duration-300 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1 px-8 py-4 text-base"
>
  Button Text
  <ArrowRight size={18} className="group-hover:translate-x-1 transition-transform" />
</a>
```

### Primary Button Specifications

- **Background:** `bg-amber-500`
- **Text Color:** `text-black` (NOT white!)
- **Font:** `font-bold` (NOT `font-mono`)
- **Sizes:**
  - Default: `px-8 py-4 text-base`
  - Large: `px-12 py-5 text-lg`
- **Hover:** `hover:bg-amber-400` with shadow glow and lift
- **Icon:** Always include ArrowRight with hover translate
- **Border Radius:** None (sharp corners)

### Secondary Button

```tsx
<button
  className="inline-flex items-center gap-3 bg-white/5 backdrop-blur-sm border border-white/20 text-white px-8 py-4 hover:bg-white/10 hover:border-amber-500/50 transition-all"
>
  Secondary Action
  <ArrowRight size={18} />
</button>
```

## Border Radius Rules

**FUNDAMENTAL RULE:** Cards, containers, and buttons use **sharp corners only** - NO rounded corners.

```tsx
// ✅ CORRECT - Sharp corners
<div className="bg-white/[0.02] border border-white/10 p-6">
  Content
</div>

// ❌ WRONG - Rounded corners
<div className="bg-white/[0.02] border border-white/10 rounded-lg p-6">
  Content
</div>
```

**Exceptions (only these):**
- Small badges/tags: `rounded-full` or `rounded-sm`
- Icons in circular containers: `rounded-full`
- Very specific decorative elements (use sparingly)

## Component Patterns

### Cards/Containers

```tsx
// Standard card (dark mode)
<div className="bg-white/[0.02] border border-white/10 p-6 hover:border-amber-500/30 transition-all duration-300 hover:-translate-y-1">
  Content
</div>

// Card with icon
<div className="bg-white/[0.02] border border-white/10 p-6">
  <div className="w-12 h-12 bg-amber-500/10 border border-amber-500/30 flex items-center justify-center mb-4">
    <Icon size={24} className="text-amber-500" />
  </div>
  <h3 className="text-lg font-semibold text-white mb-2">Title</h3>
  <p className="text-white/50 text-sm">Description</p>
</div>
```

### Links

```tsx
// Internal navigation link
<button
  onClick={() => setPage('target-page')}
  className="text-amber-500 hover:text-amber-400 transition-colors"
>
  Link text
</button>

// External link
<a
  href="https://example.com"
  target="_blank"
  rel="noopener noreferrer"
  className="text-amber-500 hover:text-amber-400 transition-colors"
>
  External link
</a>
```

### Dividers

```tsx
// Horizontal rule
<div className="border-t border-white/10" />

// Section divider with spacing
<div className="h-px bg-white/10 my-8" />
```

## Layout Constraints

| Context | Max Width | Notes |
|---------|-----------|-------|
| Blog header | 800px | Title, subtitle, meta |
| Blog featured image | 800px | Aligns with header |
| Blog article content | 680px | Narrower for readability |
| Standard page content | `max-w-5xl` | Most pages |
| Full-width grids | `max-w-6xl` | Grid layouts |
| Text-heavy sections | `max-w-4xl` | Long-form content |
| Centered CTAs | `max-w-3xl` | Call-to-action sections |

## Spacing Standards

| Element | Padding/Margin |
|---------|----------------|
| Standard sections | `py-24 px-4` |
| Hero sections | `min-h-[80vh]` with `pt-12 pb-20` |
| CTA sections | `py-32 px-4` |
| Cards | `p-6` or `p-8` |
| Card grids | `gap-4` or `gap-6` |

## Interactive Effects

### Hover States

```tsx
// Card hover
className="transition-all duration-300 hover:-translate-y-1 hover:border-amber-500/30"

// Button hover
className="transition-all duration-300 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1"

// Icon hover
className="group-hover:scale-110 transition-transform"
```

### Sweep Animation (Cards)

```css
.benefit-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(245, 158, 11, 0.08), transparent);
  transition: left 0.6s ease;
}

.benefit-card:hover::before {
  left: 100%;
}
```

## Best Practices

1. **Sharp Corners** - NO rounded corners on cards/containers (except badges/icons)
2. **Button Colors** - Primary buttons: `bg-amber-500 text-black` (NOT white text!)
3. **Typography** - Use `font-display` (Instrument Serif) for all headings
4. **Consistency** - Use established patterns; don't invent new ones
5. **Spacing** - Generous padding; content should breathe
6. **Contrast** - Use opacity variations for text hierarchy
7. **Interactivity** - Add hover states to all interactive elements
8. **Responsiveness** - Use breakpoints (`sm:`, `md:`, `lg:`) for all layouts
9. **Max Widths** - Constrain content width for readability
10. **Gradient Text** - Use `.gradient-text` class for accent words in headings

## Quick Reference

```tsx
// Standard page wrapper
<div className="min-h-screen bg-[#0a0a0a] text-white">
  
  {/* Heading with gradient accent */}
  <h1 className="font-display text-5xl md:text-7xl">
    Main Text{' '}
    <span className="gradient-text italic">Accent</span>
  </h1>

  {/* Primary button */}
  <a className="group inline-flex items-center gap-3 font-bold bg-amber-500 text-black px-8 py-4 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1">
    Button Text
    <ArrowRight size={18} className="group-hover:translate-x-1 transition-transform" />
  </a>

  {/* Card */}
  <div className="bg-white/[0.02] border border-white/10 p-6 hover:border-amber-500/30 transition-all hover:-translate-y-1">
    Content
  </div>

</div>
```
