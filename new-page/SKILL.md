---
name: new-page
description: Use this skill when creating a new page in the Ential app. Automatically handles view creation, SEO metadata, sitemap updates, routing, and type definitions. Ensures consistent structure and human-like content.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# New Page Creator

This skill provides a complete checklist and automation for creating new pages in the Ential React application.

## CRITICAL: 6-File Update Requirement

**Every new page requires updates to ALL 6 files:**

| # | File | What to Add | Why |
|---|------|-------------|-----|
| 1 | `views/[PageName].tsx` | Page component | The actual page content |
| 2 | `types.ts` | PageView type | TypeScript type safety |
| 3 | `App.tsx` | Lazy import + switch case | Routing and code splitting |
| 4 | `route-metadata.ts` | SEO metadata entry | Pre-rendering and SEO |
| 5 | `scripts/generate-sitemap.mjs` | staticRoutes entry | Sitemap generation |
| 6 | Run `npm run build` | Regenerate sitemap | Updates public/sitemap.xml |

**Missing any file = broken functionality:**
- Missing #1 = Page won't render
- Missing #2 = TypeScript errors
- Missing #3 = Page unreachable via navigation
- Missing #4 = No SEO, poor pre-rendering
- Missing #5 = Missing from sitemap

## Step-by-Step Process

### Step 1: Create View Component

Create `views/[PageName].tsx`:

```tsx
import React from 'react';
import { PageView } from '../types';

interface PageNameProps {
  setPage: (page: PageView) => void;
}

const PageName: React.FC<PageNameProps> = ({ setPage }) => {
  return (
    <div className="bg-[#0a0a0a] min-h-screen">
      {/* Page content here */}
    </div>
  );
};

export default PageName;
```

**Naming conventions:**
- File: PascalCase (e.g., `NewFeature.tsx`)
- Component: PascalCase (e.g., `NewFeature`)
- Route: kebab-case (e.g., `new-feature`)

### Step 2: Add to types.ts

Add your new page type to the `PageView` union type:

```ts
export type PageView = 'home' | 'about' | ... | 'your-new-page';
```

**Important:** Use kebab-case for the type value.

### Step 3: Add to App.tsx

#### 3a. Add lazy import (near top of file, ~line 17-57)

```tsx
const YourNewPage = lazy(() => import('./views/YourNewPage'));
```

#### 3b. Add switch case in renderContent function (~line 639-683)

```tsx
case 'your-new-page': return <YourNewPage setPage={navigateToPage} />;
```

### Step 4: Add SEO Metadata to route-metadata.ts

Add entry to `routeMetadata` object:

```ts
'/your-new-page': {
  path: '/your-new-page',
  title: 'Page Title — Ential',                    // 50-60 chars
  description: 'Compelling description.',          // 150-160 chars
  keywords: 'keyword1, keyword2, keyword3',
  canonical: `${SITE_URL}/your-new-page`,
  ogTitle: 'Page Title — Ential',
  ogDescription: 'Short description for social.',
  priority: 0.7,                                   // 0.3-1.0
  changefreq: 'monthly',                           // daily/weekly/monthly/yearly
},
```

**Priority guidelines:**
- 1.0: Homepage only
- 0.9: Core service pages
- 0.8: Important content pages
- 0.7: Secondary pages
- 0.6: Support/utility pages
- 0.3: Legal/checkout pages

### Step 5: Add to Sitemap Generator

Edit `scripts/generate-sitemap.mjs` and add to `staticRoutes` array:

```js
{ url: '/your-new-page', priority: 0.7, changefreq: 'monthly' },
```

Place it in the appropriate priority section within the array.

### Step 6: Build to Regenerate Sitemap

```bash
npm run build
```

This runs `generate-sitemap.mjs` as a prebuild step, updating `public/sitemap.xml`.

## SEO Requirements

### URL Slugs

- Lowercase with hyphens only
- 2-5 words maximum
- Descriptive and keyword-rich
- Human-readable

| Good | Bad |
|------|-----|
| `/ai-training` | `/AITraining` |
| `/book-support-call` | `/book_call` |
| `/prompt-library` | `/page123` |

### Meta Title (50-60 characters)

Format: `Primary Keyword — Secondary Info | Ential`

### Meta Description (150-160 characters)

Include:
- Primary keyword
- Value proposition
- Call-to-action (implicit or explicit)

### Keywords

5-10 relevant keywords, lowercase, comma-separated.

## Human-Like Content Guidelines

All page content must follow these rules to sound natural:

### Structure
- Write in flowing paragraphs
- Use commas instead of hyphens to separate ideas
- Only break paragraphs when changing subjects
- Vary sentence length naturally

### Tone
- Be direct when appropriate
- Avoid unnecessary metaphors
- Take positions when it makes sense
- Don't over-explain

### Restrictions
- Never use emojis
- Avoid caps lock
- Don't use bold/italics for emphasis
- Limit quotation marks
- Avoid bullet lists unless truly necessary

### Words to Avoid

Never use these AI-typical words:
- delve, dive into, journey, realm, landscape
- game-changing, cutting-edge, groundbreaking
- robust, seamless, leverage, unlock
- in today's digital age, in the realm of
- it's worth noting, importantly, furthermore
- additionally, moreover, consequently
- tapestry, navigate, embark, harness

## Component Patterns

### Hero Section

```tsx
<section className="relative pt-8 pb-32 px-6 overflow-hidden">
  <div className="max-w-7xl mx-auto relative z-10">
    <h1 className="text-5xl md:text-7xl font-serif text-white leading-tight">
      Main <span className="text-amber-500 italic">Headline</span>
    </h1>
    <p className="text-lg text-neutral-300 font-light max-w-xl">
      Supporting description text.
    </p>
    <button
      onClick={() => setPage('contact')}
      className="group px-10 py-5 bg-amber-500 text-black font-bold tracking-[0.2em] uppercase rounded-full hover:bg-amber-400 transition-all"
    >
      CTA TEXT
    </button>
  </div>
</section>
```

### Content Section

```tsx
<section className="py-32 px-6">
  <div className="max-w-7xl mx-auto">
    <div className="text-center mb-16 space-y-6">
      <h2 className="text-4xl md:text-6xl font-serif text-white">
        Section <span className="text-amber-500 italic">Title</span>
      </h2>
    </div>
    {/* Content */}
  </div>
</section>
```

### Dark/Light Backgrounds

- Dark sections: `bg-[#0a0a0a]` or `bg-[#050505]`
- Borders: `border border-white/10`
- Text: `text-white`, `text-neutral-300`, `text-neutral-400`
- Accent: `text-amber-500`

## Routing: URL to PageView Mapping

The `getPageFromPath` function in App.tsx maps URLs to PageView types.

Add your mapping (~line 389-460):

```tsx
case '/your-new-page':
  return 'your-new-page';
```

And in `getPathFromPage` (~line 462-530):

```tsx
case 'your-new-page':
  return '/your-new-page';
```

## Publishing Checklist

Run this before considering the page complete:

### Files Updated
- [ ] Created `views/[PageName].tsx` component
- [ ] Added to `types.ts` PageView type
- [ ] Added lazy import to `App.tsx`
- [ ] Added switch case in `App.tsx` renderContent
- [ ] Added URL mapping in `getPageFromPath`
- [ ] Added URL mapping in `getPathFromPage`
- [ ] Added SEO metadata to `route-metadata.ts`
- [ ] Added to `staticRoutes` in `generate-sitemap.mjs`

### SEO Verified
- [ ] Meta title is 50-60 characters
- [ ] Meta description is 150-160 characters
- [ ] Keywords are relevant and included
- [ ] Canonical URL is correct
- [ ] Priority reflects page importance
- [ ] OG title/description set for social sharing

### Build & Test
- [ ] `npm run build` completes without errors
- [ ] Page is accessible at the URL
- [ ] Navigation works correctly
- [ ] Page appears in sitemap.xml

### Content Quality
- [ ] Content follows human-like writing guidelines
- [ ] No AI-typical words or phrases
- [ ] Varied sentence structure
- [ ] Clear value proposition

---

## Quick Reference: Files to Update

```
views/[PageName].tsx      # Create new file
types.ts                  # Add to PageView type
App.tsx                   # Lazy import + switch case + URL mappings
route-metadata.ts         # SEO metadata entry
scripts/generate-sitemap.mjs  # staticRoutes entry
npm run build             # Regenerate sitemap
```

**If any step is missed, the page will not function correctly.**
