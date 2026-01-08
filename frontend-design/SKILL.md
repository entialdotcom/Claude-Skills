---
name: frontend-design
description: Create consistent, production-grade frontend pages for the Ential website. Use this skill when building new pages, components, or sections to ensure design consistency with the established visual identity.
allowed-tools: Read, Edit, Write, Glob, Grep
---

# Frontend Design for Ential

This skill guides the creation of new pages and components that maintain visual consistency with the Ential website. All designs should feel premium, modern, and distinctly "Ential" while avoiding generic AI aesthetics.

## Design Philosophy

Ential's visual identity is:
- **Premium but accessible** - High-end aesthetics without feeling exclusive
- **Technical but human** - Terminal-inspired elements balanced with warmth
- **Bold but refined** - Strong statements with elegant execution
- **Dark-forward** - Dark backgrounds as the default, with strategic light sections
- **Sharp and clean** - No rounded corners on cards/containers (sharp edges only)

## Typography System

### Font Families

| Font | Class | Usage |
|------|-------|-------|
| **Instrument Serif** | `font-display` or `font-serif` | Headlines, hero text, titles, all major headings |
| **JetBrains Mono** | `font-mono` | Body text, buttons, UI elements, labels |
| **Space Grotesk** | `font-sans` | Stats, numbers, emphasis, card titles |

### Font Import (Required in page styles)

```css
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&display=swap');
```

### Heading Patterns

```tsx
// Hero headline - Large serif with gradient accent
<h1 className="font-display text-5xl sm:text-6xl md:text-7xl lg:text-8xl leading-[1.1] mb-8">
  Unlock the Power of{' '}
  <span className="gradient-text italic">AI</span>
  <br />
  <span className="text-4xl sm:text-5xl md:text-6xl lg:text-7xl text-white/80">
    with the AI Deep Dive
  </span>
</h1>

// Section headline - Serif with gradient accent
<h2 className="font-display text-4xl md:text-5xl lg:text-6xl text-white mb-6">
  Your Ticket to <span className="gradient-text italic">Clarity & Control</span>
</h2>

// Subsection headline
<h3 className="text-2xl font-semibold text-white mb-4">Title</h3>

// Card/feature title
<h3 className="text-lg font-semibold text-white mb-2">Feature Title</h3>
```

### Gradient Text (Amber)

```css
.gradient-text {
  background: linear-gradient(135deg, #f59e0b 0%, #fbbf24 50%, #f59e0b 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

## Color Palette

### Backgrounds

| Use Case | Dark Mode | Light Mode |
|----------|-----------|------------|
| Primary background | `bg-[#0a0a0a]` | `bg-[#f5f2eb]` |
| Very dark background | `bg-[#030303]` | - |
| Secondary background | `bg-black/30` | `bg-[#faf8f4]` |
| Card background (dark) | `bg-white/[0.02]` or `bg-white/[0.03]` | `bg-[#faf8f4]` |
| Card background (subtle) | `bg-white/[0.05]` | - |

### Text Colors

| Use Case | Dark Mode | Light Mode |
|----------|-----------|------------|
| Primary text | `text-white` | `text-[#0a0a0a]` |
| Secondary text | `text-white/60` | `text-neutral-700` |
| Muted text | `text-white/40` or `text-white/50` | `text-[#7a7a7a]` |
| Accent text | `text-amber-500` | `text-amber-500` |

### Accent Colors (Amber)

```tsx
// Primary accent
className="text-amber-500"  // #f59e0b
className="bg-amber-500"      // Solid background
className="border-amber-500"   // Solid border

// Accent with transparency
className="bg-amber-500/10"        // Subtle backgrounds
className="bg-amber-500/20"        // Tags/badges
className="border-amber-500/20"    // Subtle borders
className="border-amber-500/30"    // Medium borders
className="border-amber-500/40"    // Stronger borders

// Hover states
className="hover:bg-amber-400"     // Lighter on hover
className="hover:border-amber-500/40"  // Stronger border on hover
```

## Button System

### Primary Button (Standard)

**CRITICAL:** Primary buttons use `text-black` (not white!) on amber background.

```tsx
<a
  href={url}
  className="group inline-flex items-center justify-center gap-3 font-bold bg-amber-500 text-black transition-all duration-300 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1 px-8 py-4 text-base"
>
  Button Text
  <ArrowRight size={18} className="group-hover:translate-x-1 transition-transform" />
</a>
```

### Primary Button (Large)

```tsx
<a
  href={url}
  className="group inline-flex items-center justify-center gap-3 font-bold bg-amber-500 text-black transition-all duration-300 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1 px-12 py-5 text-lg"
>
  Button Text
  <ArrowRight size={20} className="group-hover:translate-x-1 transition-transform" />
</a>
```

### Button Specifications

- **Font:** `font-bold` (NOT `font-mono`)
- **Text color:** `text-black` on amber background
- **Sizes:**
  - Default: `px-8 py-4 text-base`
  - Large: `px-12 py-5 text-lg`
- **Always include:** ArrowRight icon with hover translate animation
- **Hover effects:** Lighter amber, shadow glow, slight lift

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

**IMPORTANT:** Cards and containers use **sharp corners only** - NO rounded corners.

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

**Exception:** Only use rounded corners for:
- Small badges/tags: `rounded-full` or `rounded-sm`
- Icons in circular containers: `rounded-full`
- Very specific decorative elements

## Page Structure

### Standard Page Layout

```tsx
const NewPage: React.FC<{ setPage: (page: PageView) => void }> = ({ setPage }) => {
  return (
    <div className="min-h-screen bg-[#0a0a0a] text-white">
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&display=swap');
        
        .font-display { font-family: 'Instrument Serif', serif; }
        
        .gradient-text {
          background: linear-gradient(135deg, #f59e0b 0%, #fbbf24 50%, #f59e0b 100%);
          -webkit-background-clip: text;
          -webkit-text-fill-color: transparent;
          background-clip: text;
        }
      `}</style>

      {/* Hero Section */}
      <section className="relative min-h-[80vh] flex items-center justify-center px-4 pt-12 pb-20">
        ...
      </section>

      {/* Content Sections */}
      <section className="py-24 px-4">
        ...
      </section>

      {/* Final CTA */}
      <section className="py-32 px-4 relative overflow-hidden">
        ...
      </section>
    </div>
  );
};
```

### Section Padding Standards

| Section Type | Padding |
|--------------|---------|
| Standard content | `py-24 px-4` |
| Hero sections | `min-h-[80vh]` with `pt-12 pb-20` |
| CTA sections | `py-32 px-4` |
| Alternating sections | Use `bg-gradient-to-b from-transparent via-amber-500/[0.03] to-transparent` for subtle variation |

### Max Widths

| Content Type | Max Width |
|--------------|-----------|
| Full-width grids | `max-w-6xl mx-auto` |
| Content sections | `max-w-5xl mx-auto` |
| Text-heavy sections | `max-w-4xl mx-auto` |
| Centered CTAs | `max-w-3xl mx-auto` |

## Logo Placement

### Pages Without Header Navigation

For standalone pages without the main navigation header (e.g., landing pages, results pages, tool pages), use a large centered logo at the top:

```tsx
{/* Header - Centered logo */}
<header className="pt-8 pb-4 px-6">
  <div className="flex justify-center">
    <img src="/images/navigation/ential-logo.svg" alt="Ential" className="h-24 w-auto" />
  </div>
</header>
```

**Key specifications:**
- **Height:** `h-24` (96px) - This is the standard size for pages without navigation
- **Padding:** `pt-8 pb-4 px-6` - Generous top padding, moderate bottom
- **Alignment:** `flex justify-center` - Always centered
- **No border:** Unlike navigation headers, standalone logo headers have no bottom border
- **Not sticky:** The logo header should scroll with the page, not be fixed

### Logo Sizes by Context

| Context | Height | Usage |
|---------|--------|-------|
| Standalone page header | `h-24` | Landing pages, results pages, tools (Make, Audit results, etc.) |
| Navigation header | `h-8` to `h-10` | Main site navigation |
| Print header | `h-10` | PDF/print layouts |
| Footer | `h-8` | Site footer |

**Example pages using h-24 standalone logo:**
- `/make` - Make.com landing page
- `/audit` (results view) - Audit results page
- `/zapier`, `/n8n`, `/clickup`, `/gohighlevel` - Platform landing pages

## Component Patterns

### Hero Section (Centered)

```tsx
<section className="relative min-h-[80vh] flex items-center justify-center px-4 pt-12 pb-20 overflow-hidden">
  <div className="max-w-5xl mx-auto text-center relative z-10">
    <h1 className="font-display text-5xl sm:text-6xl md:text-7xl lg:text-8xl leading-[1.1] mb-8">
      Main Headline
      <span className="gradient-text italic">Accent Text</span>
    </h1>
    <p className="text-xl md:text-2xl text-white/60 max-w-3xl mx-auto mb-12">
      Subheadline text
    </p>
    {/* CTA buttons */}
  </div>
</section>
```

### Feature Card (Dark Background)

```tsx
<div className="bg-white/[0.02] border border-white/10 p-6 hover:border-amber-500/30 transition-all duration-300 hover:-translate-y-1 group">
  <div className="w-12 h-12 bg-amber-500/10 border border-amber-500/30 flex items-center justify-center mb-4 group-hover:bg-amber-500/20 transition-all">
    <Icon size={24} className="text-amber-500" />
  </div>
  <h3 className="text-lg font-semibold text-white mb-2">Title</h3>
  <p className="text-white/50 text-sm leading-relaxed">Description</p>
</div>
```

### Benefit Card with Hover Sweep

```tsx
<div className="benefit-card bg-white/[0.02] border border-white/10 p-6 hover:border-amber-500/30 transition-all duration-300">
  {/* Add to styles: */}
  {/* .benefit-card::before {
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
  } */}
</div>
```

### Numbered Value Cards

```tsx
<div className="bg-white/[0.02] border border-amber-500/20 p-8 text-center hover:border-amber-500/40 transition-all duration-300 hover:-translate-y-2 group">
  <div className="w-14 h-14 bg-amber-500/10 border border-amber-500/30 flex items-center justify-center mx-auto mb-6 group-hover:bg-amber-500/20 transition-all">
    <Icon size={28} className="text-amber-500" />
  </div>
  <div className="text-5xl md:text-6xl font-bold text-white mb-1">200+</div>
  <div className="text-lg font-semibold text-amber-500 mb-1">Hours Saved</div>
  <p className="text-white/60 text-sm leading-relaxed">Description</p>
</div>
```

### Before/After Comparison

```tsx
<div className="grid lg:grid-cols-2 gap-6">
  {/* Before */}
  <div className="bg-gradient-to-br from-red-500/[0.05] to-transparent border border-red-500/20 p-8">
    <div className="absolute top-4 right-4 text-xs font-bold uppercase tracking-widest text-red-500/50">Before</div>
    <h3 className="text-2xl font-semibold text-white mb-6">Where You Are Now</h3>
    <ul className="space-y-4">
      <li className="flex items-start gap-3">
        <span className="text-red-500 mt-0.5 text-lg">✕</span>
        <span className="text-white/60">Problem point</span>
      </li>
    </ul>
  </div>

  {/* After */}
  <div className="bg-gradient-to-br from-amber-500/[0.1] to-transparent border border-amber-500/30 p-8">
    <div className="absolute top-4 right-4 text-xs font-bold uppercase tracking-widest text-amber-500">After</div>
    <h3 className="text-2xl font-semibold text-amber-400 mb-6">Where You'll Be</h3>
    <ul className="space-y-4">
      <li className="flex items-start gap-3">
        <span className="text-amber-500 mt-0.5 text-lg">✓</span>
        <span className="text-white">Solution point</span>
      </li>
    </ul>
  </div>
</div>
```

### Pricing Table

```tsx
<div className="bg-[#0a0a0a] border-2 border-amber-500/40 relative overflow-hidden">
  {/* Header */}
  <div className="bg-gradient-to-r from-amber-500 to-amber-600 p-6 text-center">
    <h3 className="text-2xl font-bold text-black">Product Name</h3>
    <p className="text-black/70">Description</p>
  </div>

  <div className="p-8 md:p-12">
    {/* Price */}
    <div className="text-center mb-10">
      <div className="inline-flex items-baseline gap-3 mb-2">
        <span className="text-2xl text-white/40 line-through">$2,500</span>
        <span className="text-6xl md:text-7xl font-bold text-white">$750</span>
      </div>
      <p className="text-amber-500 text-sm font-semibold">Save $1,750 Today</p>
    </div>

    {/* Features list */}
    <div className="grid md:grid-cols-2 gap-x-8 gap-y-4 mb-10">
      {features.map((feature, i) => (
        <div key={i} className="flex items-center gap-4 py-3 border-b border-white/10">
          <div className="w-10 h-10 bg-amber-500/10 border border-amber-500/30 flex items-center justify-center shrink-0">
            <Check size={18} className="text-amber-500" />
          </div>
          <div className="flex-1">
            <span className="text-white text-sm">{feature.text}</span>
          </div>
          <span className="text-amber-500/70 text-sm font-semibold">{feature.value}</span>
        </div>
      ))}
    </div>

    {/* CTA */}
    <div className="text-center">
      <a href={url} className="group inline-flex items-center justify-center gap-3 w-full md:w-auto bg-amber-500 text-black px-12 py-5 text-lg font-bold transition-all duration-300 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1">
        YES! I Want This
        <ArrowRight size={20} className="group-hover:translate-x-1 transition-transform" />
      </a>
    </div>
  </div>
</div>
```

## Animation Patterns

### Fade In on Load

```css
.fade-in {
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease forwards;
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.delay-1 { animation-delay: 0.1s; }
.delay-2 { animation-delay: 0.2s; }
.delay-3 { animation-delay: 0.3s; }
.delay-4 { animation-delay: 0.4s; }
```

### Hover Transitions

```tsx
// Card hover
className="transition-all duration-300 hover:-translate-y-1 hover:border-amber-500/30"

// Button hover
className="transition-all duration-300 hover:bg-amber-400 hover:shadow-[0_0_60px_rgba(245,158,11,0.4)] hover:-translate-y-1"

// Icon hover
className="group-hover:scale-110 transition-transform"
```

### Cursor Glow Effect (Optional, below header only)

```tsx
// Only show when cursor is below header (viewportY > 120)
{mousePosition.viewportY > 120 && (
  <div 
    className="pointer-events-none fixed w-[500px] h-[500px] rounded-full blur-[200px] bg-amber-500/[0.07] transition-all duration-500 ease-out z-0"
    style={{
      left: mousePosition.viewportX - 250,
      top: mousePosition.viewportY - 250,
    }}
  />
)}
```

## Section Checklist

When creating a new page, include these sections in order:

1. **Hero Section** - Centered, bold headline, primary CTA
2. **Problem/Reality** - Address pain points
3. **Solution/Benefits** - Show value with stats and cards
4. **What You'll Get** - Detailed breakdown
5. **Transformation** - Before/After comparison
6. **Pricing** - Clear pricing table with value breakdown
7. **FAQ** - Accordion-style questions
8. **Final CTA** - Centered, strong copy

## Common Imports

```tsx
import React, { useState, useEffect, useRef } from 'react';
import { ArrowRight, Check, ChevronDown, Clock, Target, Zap, Users } from 'lucide-react';
import { PageView } from '../types';
```

## Human-Sounding Copy Rules

**CRITICAL:** All page copy must follow these rules to sound human, not robotic. These rules apply to headlines, descriptions, CTAs, and all written content on frontend pages.

### Structure and Formatting
- Avoid separating topics with hyphens. Don't use the [topic] - [explanation] format.
- Write in flowing paragraphs like normal conversation.
- Use commas instead of hyphens to separate ideas.
- Only break paragraphs when actually changing subjects.

### Tone and Voice
- Maintain natural irregularity in sentence length. Alternate between short and long sentences.
- Sometimes be direct. Other times elaborate more, but don't force it.
- Avoid unnecessary metaphors and poetic comparisons for simple concepts.

### Conversational Behaviour
- Disagree when it makes sense. Question incorrect premises.
- Don't automatically validate everything. If something is wrong, point it out naturally.
- Avoid starting with compliments or hype.

### Specific Restrictions
- Never use emojis in copy (except where explicitly requested).
- Avoid caps lock completely.
- Drastically limit the use of quotation marks for emphasis.
- Avoid bullet lists in marketing copy unless truly necessary.

### Language and Style
- Vary between formal and informal as context demands.
- Use contractions when appropriate.
- Avoid over-explaining your reasoning process.
- Don't announce what you're going to do before doing it.

### Content Guidelines
- Be specific rather than generic.
- Take positions when appropriate.
- Avoid always seeking artificial balance between viewpoints.
- Don't hesitate to be brief when the point is simple.
- Resist the temptation to always add extra context or elaborate unnecessarily.

### Words and Phrases to Avoid

**Never use these AI-typical phrases:**
- additionally, alternatively, amongst, arguably, as a professional, as previously mentioned, as well as, bridging, bustling, changing the game, compelling, consequently, crucial, cutting-edge, daunting, delve into, designed to enhance, dilemma, dive, dive into, diving, embark, elevate, emphasize, ensure, essentially, essential, ever-evolving, everchanging, evolving, excels, expand, expanding, fancy, firstly, foster, foundations, furthermore, game changer, game-changing, given that, gossamer, groundbreaking, harness, imagine, immense, importantly, in conclusion, in contrast, in order to, in summary, in the quest, in the realm of, in the world of, in today's digital age, in today's digital era, indeed, indelible, intense, it is advisable, it's essential to, it's important to note, it's worth noting that, journey, keen, landscape, labyrinth, let's, mastering, metropolis, meticulous, meticulously, moreover, my friend, navigating, nestled, not only, notably, orchestrate, orchestrating, paced, picture this, paramount, power, pressure, profoundly, promptly, pursuit, quest, rapidly, realm, relentless, remember that..., remnant, reshape, reshaping, reverberate, revolutionize, robust, seismic, shall, sights unseen, sounds unheard, specifically, struggled, subsequently, take a dive into, tapestry, tailored, testament, the world of, there are a few considerations, thrilled, thus, to consider, to put it simply, to summarize, today's, towards, transformative, ultimately, underpins, underscore, unleash, unlock the secrets, unprecedented, unveil the secrets, vibrant, vital, whispering, when it comes to, world, you may want to, understanding, alright, game changer, It is advisable, comprehensive, empower, seamless, leverage, unlock, transform (as a verb for marketing speak).

**Avoid concepts like:**
- "In today's environment"
- "In today's business world"
- "Rapidly changing"
- "In the competitive business environment"
- "Being inclusive"

**Before publishing:** Review all copy to ensure it adheres to these rules. The goal is to sound like a human wrote it, not a chatbot.

## Best Practices

1. **Consistency** - Use established patterns; don't invent new ones unless necessary
2. **Sharp Corners** - NO rounded corners on cards/containers (except badges/icons)
3. **Button Colors** - Primary buttons: `bg-amber-500 text-black` (NOT white text!)
4. **Typography** - Use `font-display` (Instrument Serif) for all headings
5. **Spacing** - Generous padding; content should breathe
6. **Contrast** - Use opacity variations (`text-white/60`, `text-white/40`) for hierarchy
7. **Interactivity** - Add hover states and transitions to all interactive elements
8. **Responsiveness** - Use `sm:`, `md:`, `lg:` breakpoints for all layouts
9. **Max Widths** - Constrain content width for readability
10. **Gradient Text** - Use `.gradient-text` class for accent words in headings
11. **Human Copy** - Follow the Human-Sounding Copy Rules above for all written content
