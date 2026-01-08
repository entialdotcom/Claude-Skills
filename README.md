# Claude Skills Collection

A curated collection of Claude Code skills for building and maintaining the Ential website. These skills provide structured guidance for common development tasks, ensuring consistency across the codebase.

## Skills Overview

| Skill | Purpose |
|-------|---------|
| [blog-post-editor](#blog-post-editor) | Create and manage blog posts with SEO optimization |
| [brand-guidelines](#brand-guidelines) | Visual identity: fonts, colors, and design patterns |
| [frontend-design](#frontend-design) | Build consistent, production-grade pages |
| [job-descriptions](#job-descriptions) | Manage careers page job listings |
| [mobile-responsiveness](#mobile-responsiveness) | Ensure proper mobile optimization |
| [new-page](#new-page) | Create new pages with routing and SEO |
| [skill-sync](#skill-sync) | Sync skills to this backup repository |

---

## blog-post-editor

**Use when:** Creating, editing, or managing blog posts for The Canonical Times blog.

### Key Features
- 4-file update requirement (blogPosts.tsx, Blog.tsx, BlogPost.tsx, route-metadata.ts)
- Automatic date formatting (Brisbane timezone)
- SEO validation (meta titles, descriptions, keywords, tags)
- Human-sounding writing guidelines with AI-typical phrases to avoid
- Headline formulas for varied, engaging titles

### Critical Rules
- Every blog post requires an image in both `blogPosts.tsx` and `Blog.tsx`
- All h2 headings must use `text-amber-500`
- Sitemap auto-generates from slugs during build

---

## brand-guidelines

**Use when:** Styling components, creating pages, or ensuring visual consistency.

### Typography
| Font | Usage | Tailwind Class |
|------|-------|----------------|
| Instrument Serif | Headings, hero text | `font-display` or `font-serif` |
| JetBrains Mono | Body text, UI elements | `font-mono` |
| Space Grotesk | Stats, numbers, emphasis | `font-sans` |

### Color Palette
- **Primary dark:** `#0a0a0a`
- **Accent:** Amber scale (`amber-400` through `amber-600`)
- **Text:** White with opacity variations (`text-white/60`, `text-white/40`)

### Critical Rules
- Sharp corners only on cards/containers (no `rounded-lg`)
- Primary buttons: `bg-amber-500 text-black` (NOT white text)
- Use `.gradient-text` class for accent words in headings

---

## frontend-design

**Use when:** Building new pages, components, or sections that need to match the Ential visual identity.

### Design Philosophy
- Premium but accessible
- Technical but human
- Bold but refined
- Dark-forward with strategic light sections
- Sharp and clean (no rounded corners)

### Component Library
- Hero sections (centered with gradient text)
- Feature cards with hover effects
- Before/After comparisons
- Pricing tables
- Numbered value cards

### Human-Sounding Copy Rules
Includes comprehensive guidelines for writing copy that avoids AI-typical phrases and sounds natural.

---

## job-descriptions

**Use when:** Creating or editing job descriptions for the Ential careers page.

### File Structure
- Source files: `public/jds/*.md`
- Naming pattern: `ai-[role-name]-upwork.md`
- URLs generated from slugs: `/careers/ai-automation-engineer`

### Required Section Order
1. Title
2. About Ential
3. Role Overview
4. Why Join Us?
5. What You'll Do
6. What We're Looking For (includes High Agency + Remote Setup requirements)
7. Work Details
8. How to Apply
9. Critical Instruction

### Key Features
- Automatic amber styling for all headings
- Emoji removal (except warning icons)
- Callout boxes for critical/important sections
- Automatic content filtering

---

## mobile-responsiveness

**Use when:** Building new pages, reviewing for mobile issues, or fixing responsiveness problems.

### Breakpoint System
| Prefix | Min Width | Target |
|--------|-----------|--------|
| (none) | 0px | Mobile phones |
| `sm:` | 640px | Large phones |
| `md:` | 768px | Tablets |
| `lg:` | 1024px | Laptops |
| `xl:` | 1280px | Desktops |

### Core Principles
- Mobile-first approach
- No horizontal overflow
- Touch-friendly (44px minimum touch targets)
- Readable text on all screen sizes

### Quick Size Scaling
| Desktop | Mobile |
|---------|--------|
| `text-6xl` | `text-2xl` |
| `p-8` | `p-4` |
| `py-32` | `py-16` |
| `gap-8` | `gap-4` |

---

## new-page

**Use when:** Creating a new page in the Ential React application.

### 6-File Update Requirement

| # | File | Purpose |
|---|------|---------|
| 1 | `views/[PageName].tsx` | Page component |
| 2 | `types.ts` | PageView type |
| 3 | `App.tsx` | Lazy import + routing |
| 4 | `route-metadata.ts` | SEO metadata |
| 5 | `generate-sitemap.mjs` | Sitemap entry |
| 6 | `npm run build` | Regenerate sitemap |

### SEO Guidelines
- Meta title: 50-60 characters
- Meta description: 150-160 characters
- URL slugs: lowercase, hyphens, 2-5 words

### Priority Scale
- 1.0: Homepage
- 0.9: Core service pages
- 0.8: Important content
- 0.7: Secondary pages
- 0.6: Support/utility
- 0.3: Legal/checkout

---

## skill-sync

**Use when:** After creating or updating any skill to keep this backup repository in sync.

### Sync Commands

```bash
# Sync single skill
cp -r /path/to/source/.claude/skills/<skill-name> /path/to/ClaudeSkills/

# Sync all skills
cp -r /path/to/source/.claude/skills/* /path/to/ClaudeSkills/

# Verify sync
diff -rq /path/to/source/.claude/skills/ /path/to/ClaudeSkills/
```

---

## Usage

Each skill is stored in its own folder with a `SKILL.md` file containing detailed instructions. Claude Code automatically loads these skills based on the task context.

### Skill Structure

```
ClaudeSkills/
├── blog-post-editor/
│   └── SKILL.md
├── brand-guidelines/
│   └── SKILL.md
├── frontend-design/
│   └── SKILL.md
├── job-descriptions/
│   └── SKILL.md
├── mobile-responsiveness/
│   └── SKILL.md
├── new-page/
│   └── SKILL.md
├── skill-sync/
│   └── SKILL.md
└── README.md
```

## License

MIT