---
name: mobile-responsiveness
description: Ensure pages are properly optimized for mobile devices. Use this skill when building new pages, reviewing existing pages for mobile issues, or fixing mobile responsiveness problems. Checks for proper breakpoints, text sizing, overflow issues, and touch-friendly interactions.
allowed-tools: Read, Edit, Write, Glob, Grep
---

# Mobile Responsiveness Guidelines for Ential

This skill ensures all pages and components are properly optimized for mobile devices. Apply these guidelines when building new pages or fixing mobile issues.

## Core Principles

1. **Mobile-first approach** - Design for mobile, then scale up
2. **No horizontal overflow** - Content must never exceed viewport width
3. **Touch-friendly** - All interactive elements must be easily tappable
4. **Readable text** - Font sizes must be legible on small screens
5. **Proper spacing** - Adequate padding and margins for mobile

## Breakpoint System

Use Tailwind's responsive prefixes consistently:

| Prefix | Min Width | Target Devices |
|--------|-----------|----------------|
| (none) | 0px | Mobile phones (default) |
| `sm:` | 640px | Large phones, small tablets |
| `md:` | 768px | Tablets |
| `lg:` | 1024px | Small laptops |
| `xl:` | 1280px | Desktops |

### Example Usage

```tsx
// Mobile-first responsive text
<h1 className="text-2xl sm:text-3xl md:text-4xl lg:text-6xl">
  Headline
</h1>

// Mobile-first responsive padding
<section className="py-16 md:py-32 px-4 md:px-6">
  Content
</section>

// Mobile-first responsive grid
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
  Items
</div>
```

## Typography Sizing

### Headlines

| Element | Mobile | Tablet (md) | Desktop (lg+) |
|---------|--------|-------------|---------------|
| Hero H1 | `text-2xl` or `text-3xl` | `text-4xl` or `text-5xl` | `text-6xl` to `text-8xl` |
| Section H2 | `text-2xl` | `text-3xl` or `text-4xl` | `text-5xl` or `text-6xl` |
| Card H3 | `text-base` or `text-lg` | `text-lg` or `text-xl` | `text-xl` |
| Labels | `text-[10px]` or `text-xs` | `text-xs` or `text-sm` | `text-sm` |

### Body Text

| Element | Mobile | Tablet+ |
|---------|--------|---------|
| Body text | `text-sm` or `text-base` | `text-base` or `text-lg` |
| Descriptions | `text-xs` or `text-sm` | `text-sm` or `text-base` |
| Captions | `text-[10px]` or `text-xs` | `text-xs` |

### Letter Spacing

Reduce letter-spacing on mobile for better readability:

```tsx
// Letter spacing that scales
<span className="tracking-wider md:tracking-widest uppercase">
  Label Text
</span>

// Button letter spacing
<button className="tracking-[0.1em] md:tracking-[0.2em]">
  Button
</button>
```

## Spacing Standards

### Section Padding

```tsx
// Standard section
<section className="py-16 md:py-32 px-4 md:px-6">

// Hero section
<section className="pt-6 md:pt-8 pb-16 md:pb-32 px-4 md:px-6">

// Compact section
<section className="py-12 md:py-20 px-4 md:px-6">
```

### Element Spacing

| Element | Mobile | Desktop |
|---------|--------|---------|
| Section gaps | `gap-4` | `gap-6` or `gap-8` |
| Card padding | `p-4` | `p-6` or `p-8` |
| Content margins | `mb-8` or `mb-10` | `mb-16` or `mb-20` |
| Icon margins | `mb-3` | `mb-4` or `mb-6` |

## Preventing Overflow

### Container Rules

```tsx
// Main page container - ALWAYS include these
<div className="overflow-x-hidden w-full max-w-[100vw]">
  Page content
</div>

// Sections that might overflow
<section className="overflow-hidden">
  Content with animations or absolute positioning
</section>
```

### Common Overflow Fixes

```tsx
// Remove max-width constraints that exceed viewport
// BAD: max-w-xl on mobile (576px > 430px viewport)
<p className="max-w-xl">Text</p>

// GOOD: No max-width or responsive max-width
<p className="max-w-full lg:max-w-xl">Text</p>

// Scrollable containers for wide content
<div className="overflow-x-auto -mx-4 px-4 md:mx-0 md:px-0">
  <div style={{ minWidth: 'max-content' }}>
    Wide content like tables or step indicators
  </div>
</div>

// Text that should wrap
<span className="break-words">Long text that might overflow</span>

// Flex items that should shrink
<div className="flex items-center gap-2">
  <Icon className="shrink-0" />
  <span className="truncate">Text that truncates</span>
</div>
```

### Absolute Positioning

Avoid negative positioning that causes overflow on mobile:

```tsx
// BAD - Can overflow on mobile
<div className="absolute -top-3 -right-3">Badge</div>

// GOOD - Inside on mobile, outside on desktop
<div className="absolute top-2 right-2 md:-top-3 md:-right-3">Badge</div>
```

## Buttons

### Standard Responsive Button

```tsx
<button className="
  group
  px-6 md:px-10
  py-4 md:py-5
  bg-amber-500
  text-black
  font-bold
  tracking-[0.1em] md:tracking-[0.2em]
  uppercase
  rounded-full
  text-sm md:text-base
  w-full sm:w-auto
  inline-flex items-center justify-center gap-2 md:gap-3
">
  Button Text
  <ArrowRight size={16} className="md:w-[18px] md:h-[18px] shrink-0" />
</button>
```

### Key Button Rules

- Use `w-full sm:w-auto` for buttons that stack on mobile
- Reduce padding: `px-6` on mobile, `px-10` on desktop
- Reduce icon sizes: `size={16}` on mobile, larger on desktop
- Use `shrink-0` on icons to prevent squishing

## Cards

### Standard Responsive Card

```tsx
<div className="
  bg-[#0f0f0f]
  border border-white/10
  rounded-xl md:rounded-2xl
  p-4 md:p-6 lg:p-8
">
  <div className="w-10 md:w-12 h-10 md:h-12 rounded-lg md:rounded-xl">
    <Icon size={20} className="md:w-6 md:h-6" />
  </div>
  <h3 className="text-base md:text-lg lg:text-xl mb-2 md:mb-3">Title</h3>
  <p className="text-xs md:text-sm">Description</p>
</div>
```

## Grids

### Standard Responsive Grid

```tsx
// 4-column layout
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 md:gap-6">

// 3-column layout
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">

// 2-column layout
<div className="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-8">
```

### Grid with Scrollable Alternative

For complex content that can't stack well:

```tsx
<div className="overflow-x-auto -mx-4 px-4 md:mx-0 md:px-0">
  <div className="grid grid-cols-4 gap-2 md:gap-4 min-w-[600px] md:min-w-0">
    Items that scroll horizontally on mobile
  </div>
</div>
```

## Icons

### Responsive Icon Sizing

```tsx
// Standard approach
<Icon size={16} className="md:w-5 md:h-5 lg:w-6 lg:h-6" />

// With shrink protection
<Icon size={16} className="shrink-0" />

// In flex containers
<div className="flex items-center gap-2">
  <Icon size={14} className="shrink-0 text-amber-500" />
  <span>Label</span>
</div>
```

## Interactive Elements

### Touch-Friendly Sizing

Minimum touch target: 44x44px

```tsx
// Good touch target
<button className="w-12 h-12 md:w-10 md:h-10">
  <Icon size={20} />
</button>

// Increased hit area with padding
<button className="p-3 -m-3">
  <Icon size={16} />
</button>
```

## Hiding/Showing Elements

```tsx
// Hide on mobile, show on desktop
<div className="hidden md:block">Desktop only</div>

// Show on mobile, hide on desktop
<div className="block md:hidden">Mobile only</div>

// Hide scroll indicator on mobile
<div className="hidden md:flex">Scroll indicator</div>
```

## Common Mobile Issues Checklist

When reviewing a page for mobile responsiveness, check for:

### Layout Issues
- [ ] No horizontal scroll on any viewport size
- [ ] All content visible without cutoff
- [ ] Proper stacking of columns on mobile
- [ ] Grids collapse to single column when needed

### Typography Issues
- [ ] All text readable (minimum 12px)
- [ ] Headlines don't overflow
- [ ] Long words break properly
- [ ] Letter-spacing reduced on mobile

### Spacing Issues
- [ ] Adequate padding on mobile (minimum `px-4`)
- [ ] Section padding scaled down (`py-16` vs `py-32`)
- [ ] Element gaps reduced on mobile

### Interactive Issues
- [ ] Buttons wide enough to tap
- [ ] Touch targets at least 44px
- [ ] No hover-only interactions
- [ ] Forms usable on mobile

### Component Issues
- [ ] Cards properly sized
- [ ] Icons not oversized
- [ ] Images responsive
- [ ] Modals/popups fit screen

## Global CSS Override (Emergency Fix)

If overflow issues persist, add this CSS:

```css
@media (max-width: 768px) {
  .page-container * {
    max-width: 100%;
    box-sizing: border-box;
  }
  .page-container section {
    overflow-x: hidden;
  }
}
```

## Testing Requirements

Before considering a page mobile-ready:

1. Test on iPhone SE (375px) - smallest common viewport
2. Test on iPhone 14 Pro Max (430px) - large phone
3. Test on iPad (768px) - tablet breakpoint
4. Verify no horizontal scroll at any size
5. Verify all text is readable
6. Verify all buttons are tappable
7. Verify all content is visible

## Example: Converting Desktop-Only Component

### Before (Desktop-only)

```tsx
<div className="grid grid-cols-4 gap-8 p-8">
  <div className="w-16 h-16">
    <Icon size={32} />
  </div>
  <h3 className="text-xl mb-4">Title</h3>
  <p className="text-base">Long description text</p>
</div>
```

### After (Mobile-responsive)

```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 md:gap-8 p-4 md:p-8">
  <div className="w-10 md:w-16 h-10 md:h-16">
    <Icon size={20} className="md:w-8 md:h-8" />
  </div>
  <h3 className="text-base md:text-xl mb-2 md:mb-4">Title</h3>
  <p className="text-xs md:text-base">Long description text</p>
</div>
```

## Quick Reference

### Size Scaling Patterns

| Desktop | Mobile |
|---------|--------|
| `text-6xl` | `text-2xl` or `text-3xl` |
| `text-xl` | `text-base` |
| `text-base` | `text-sm` or `text-xs` |
| `p-8` | `p-4` |
| `py-32` | `py-16` |
| `gap-8` | `gap-4` |
| `w-16` | `w-10` or `w-12` |
| `size={32}` | `size={20}` |
| `rounded-2xl` | `rounded-xl` |
| `tracking-widest` | `tracking-wider` |
