---
name: blog-post-editor
description: Use this skill when creating, editing, or managing blog posts for The Canonical Times. Handles blog post structure, styling, headings, formatting, and file updates for proper navigation. Includes automatic date formatting and SEO validation.
allowed-tools: Read, Edit, Write, Glob, Grep
---

# Blog Post Editor

This skill provides guidelines for creating and editing blog posts for The Canonical Times blog.

## ⚠️ CRITICAL: 4-File Update Requirement

**Every new blog post requires updates to ALL 4 files:**

| # | File | What to Add | Why |
|---|------|-------------|-----|
| 1 | `data/blogPosts.tsx` | Full post content & metadata | Post data source |
| 2 | `views/Blog.tsx` | ARTICLES entry + slug maps | Blog listing page |
| 3 | `views/BlogPost.tsx` | tickerItems entry | News ticker on posts |
| 4 | `route-metadata.ts` | SEO metadata entry | Pre-rendering & SEO |

**Sitemap:** Auto-generated from `blogPosts.tsx` slugs during build (no manual update needed).

**Missing any file = broken functionality:**
- Missing #1 = Post won't load
- Missing #2 = Post won't appear in blog listing
- Missing #3 = Ticker won't show post
- Missing #4 = Post won't be pre-rendered (bad SEO)

## Automatic Date Formatting

**IMPORTANT:** All blog posts use Brisbane, Australia timezone (AEST/AEDT) for dates.

### Date Formats

| Field | Format | Example |
|-------|--------|---------|
| `date` in blogPosts.tsx | Full month name | `December 30, 2025` |
| `modifiedDate` in blogPosts.tsx | Full month name | `December 30, 2025` |
| `date` in Blog.tsx ARTICLES | Abbreviated | `Dec 30, 2025` |

### Getting Today's Date (Brisbane Time)

When creating a new post, automatically use today's date in Brisbane timezone:

```javascript
// Brisbane is UTC+10 (AEST) or UTC+11 (AEDT during daylight saving)
const brisbaneDate = new Date().toLocaleString('en-AU', {
  timeZone: 'Australia/Brisbane',
  year: 'numeric',
  month: 'long',  // or 'short' for abbreviated
  day: 'numeric'
});
// Result: "30 December 2025" → reformat to "December 30, 2025"
```

**Always set both `date` and `modifiedDate` to today's Brisbane date when publishing.**

## File Locations

Blog posts require updates in **FOUR files**:

| File | Purpose |
|------|---------|
| `data/blogPosts.tsx` | Full blog post content and metadata |
| `views/Blog.tsx` | Blog listing page (ARTICLES array, slug mapping) |
| `views/BlogPost.tsx` | Individual post page (ticker items array) |
| `route-metadata.ts` | SEO metadata for pre-rendering |

**Images** should be saved to `public/images/blog/` and referenced in BOTH data files.

**Sitemap** is auto-generated from `blogPosts.tsx` slugs during build - no manual update needed.

**CRITICAL:** Every blog post MUST have an image. The image path must be added to:
1. `data/blogPosts.tsx` as `featuredImage: '/images/blog/image-name.png'`
2. `views/Blog.tsx` in the ARTICLES array as `image: '/images/blog/image-name.png'`

**Both locations are required** - the image will not display on the blog listing page if missing from Blog.tsx, and will not display on the individual post page if missing from blogPosts.tsx.

## Layout Constraints

**IMPORTANT:** All blog post elements must respect these max-widths:

| Element | Max Width | Notes |
|---------|-----------|-------|
| Header (title, subtitle, meta) | 800px | Set in `BlogPost.tsx` |
| Featured image | 800px | Aligns with header |
| Stats callout | 800px | Contained within wrapper |
| Article content | 680px | Narrower for readability |

Never use full-width elements that break this layout.

## SEO Requirements

### URL Slugs

Blog post slugs MUST be:
- **Lowercase** with hyphens (no underscores or spaces)
- **Descriptive** - include primary keyword
- **Concise** - 3-8 words maximum
- **Readable** - makes sense to humans
- **Keyword-first** - lead with the main topic

| Quality | Example | Issue |
|---------|---------|-------|
| Good | `i-asked-chatgpt-to-write-my-goals` | Descriptive, keyword-rich |
| Good | `bulk-delete-linkedin-messages-script` | Action + platform + type |
| Bad | `post-123` | Not descriptive |
| Bad | `chatgpt_goals_2026` | Uses underscores |
| Bad | `My-New-Post` | Uppercase letters |

### Image File Names (SEO-Critical)

Image files MUST follow these rules:

| Rule | Good Example | Bad Example |
|------|--------------|-------------|
| Lowercase only | `chatgpt-goals.png` | `ChatGPT-Goals.png` |
| Hyphens, no spaces | `marketing-dashboard.png` | `marketing dashboard.png` |
| Descriptive names | `linkedin-bulk-delete-console.png` | `IMG_2847.png` |
| Include context | `chatgpt-goals-output.png` | `screenshot.png` |
| Match slug theme | `chatgpt-goals-featured.png` | `image1.png` |

**Naming pattern:** `[topic]-[descriptor]-[type].png`
- `chatgpt-goals-output.png`
- `linkedin-messages-before-after.png`
- `automation-workflow-diagram.png`

### Meta Title (SEO)

| Rule | Requirement |
|------|-------------|
| Length | 50-60 characters (max 60) |
| Format | `Primary Keyword - Secondary Info \| Ential` |
| Include | Main keyword near the beginning |

**Good:** `I Asked ChatGPT to Write My Goals - Here's What Happened | Ential`
**Bad:** `Blog Post About Goals` (too vague, no brand)

### Meta Description (SEO)

| Rule | Requirement |
|------|-------------|
| Length | 150-160 characters (max 160) |
| Include | Primary keyword, value proposition, call-to-action |
| Tone | Compelling, benefit-focused |

**Good:** `I gave ChatGPT one prompt and it revealed uncomfortable truths about my ambitions. Here's the full output and what I learned about AI-assisted self-reflection.`
**Bad:** `A blog post about ChatGPT and goals.` (too short, no value)

### Keywords Array (SEO)

| Rule | Requirement |
|------|-------------|
| Count | 5-10 keywords per post |
| Types | Mix of short-tail and long-tail |
| Relevance | Must appear in content |
| Format | Lowercase, can include spaces |

```tsx
keywords: [
  'chatgpt goals',           // Primary keyword
  'ai goal setting',         // Related topic
  'chatgpt prompts',         // Tool-specific
  '2026 goals',              // Time-specific
  'ai self reflection',      // Long-tail
  'personal development ai', // Long-tail
]
```

### Tags (Display + SEO)

| Rule | Requirement |
|------|-------------|
| Count | 3-5 tags per post |
| Format | Title Case for display |
| Purpose | Category + topic classification |
| Unique | No duplicate meanings |

```tsx
tags: ['ChatGPT', 'Goal Setting', 'AI Tools', 'Personal Development']
```

**Good tags:** Specific, searchable, category-relevant
**Bad tags:** Generic (`Tech`), redundant (`AI`, `Artificial Intelligence`)

## Headline Formulas

**CRITICAL:** Blog post titles must use varied headline formulas. Never use the same pattern for multiple posts. Avoid the two-sentence format (e.g., "I Did X. Here's What Happened.") as it sounds AI-generated.

### Listicle Formulas
- **The [Number] Ways to [Achieve Goal]:** "10 Ways to Boost Your Productivity This Week"
- **[Number] [Secrets/Mistakes/Tips] You Didn't Know About [Topic]:** "7 Hidden SEO Mistakes That Are Killing Your Traffic"
- **The Top [Number] [Items] for [Audience/Goal]:** "The Top 5 Productivity Apps for Freelancers"

### How-To & Guide Formulas
- **How to [Achieve Desired Result] Without [Pain Point]:** "How to Learn a New Language Without Flashcards"
- **The Ultimate Guide to [Topic] for [Audience]:** "The Ultimate Guide to Starting a Blog for Beginners"
- **How [Industry] Is [Doing Something] — And How to Fix It:** "How Social Media Is Hijacking Your Attention — And How to Take It Back"
- **How to [Achieve Result] in [X] Steps:** "How to Delete Thousands of LinkedIn Messages in 15 Minutes"

### Curiosity & Question Formulas
- **The Surprising Truth About [Topic]:** "The Surprising Truth About Intermittent Fasting"
- **What [Audience] Doesn't Know About [Topic]:** "What Your Boss Doesn't Want You to Know About Raises"
- **Are You Still [Painful Thing]?:** "Are You Still Making These Common Grammar Mistakes?"

### Benefit-Driven & Problem/Solution Formulas
- **[Threat/Problem]: [Number] Quick Fixes:** "Burnout: 3 Quick Tips to Reclaim Your Energy"
- **[Number] Little Known [Things] That Could Be Causing Your [Negative Outcome]:** "9 Little-Known Nutrients Causing Your Blood Sugar Spikes"
- **Why [X] Is More Important Than You Think:** "Why Daily Journaling Is More Important Than You Realize"

### Authority & Social Proof Formulas
- **A Day in the Life of a [Profession]:** "A Day in the Life of a Content Marketing Manager"
- **What [Expert] Taught Me About [Topic]:** "What My First Year as a CEO Taught Me About Leadership"
- **What [X] Taught Me About [Topic]:** "What ChatGPT Taught Me About Identity and Ambition"

### Rules for Headlines
1. **Vary formulas** - Don't use the same formula for consecutive posts
2. **Avoid two-sentence patterns** - "I Did X. Here's What Happened." sounds robotic
3. **Be specific** - Include numbers, timeframes, or concrete details when possible
4. **Promise value** - Headlines should clearly communicate what the reader will learn
5. **Match content style** - Use How-To for tutorials, What X Taught Me for personal stories, etc.

## Creating a New Blog Post

**⚠️ CRITICAL REMINDER:** Every blog post MUST include an image in BOTH files:
- `featuredImage` in `data/blogPosts.tsx` (for individual post page)
- `image` in `views/Blog.tsx` ARTICLES array (for blog listing page)

Both must use the same image path. If either is missing, the image will not display correctly.

### Step 1: Add to `data/blogPosts.tsx`

```tsx
{
  id: 'unique-id',                    // Unique identifier
  slug: 'seo-friendly-url-slug',      // URL path (lowercase, hyphens)
  title: "Post Title Here",
  subtitle: "Compelling subtitle that hooks the reader.",
  category: 'category-id',
  categoryLabel: 'Category Name',
  date: 'December 30, 2025',          // Today's Brisbane date (full format)
  modifiedDate: 'December 30, 2025',  // Same as date for new posts
  readTime: '6 min read',
  wordCount: 720,
  author: 'Ryan Drake',
  authorInitial: 'R',
  authorData: {
    name: 'Ryan Drake',
    initial: 'R',
    role: 'Founder, Ential',
    url: 'https://ryandrake.com',
  },
  tags: ['Tag1', 'Tag2', 'Tag3'],     // 3-5 Title Case tags
  ticker: 'new',                      // 'breaking' | 'hot' | 'new' | undefined
  tickerText: "Ticker text here",
  placeholder: '???',
  featuredImage: '/images/blog/topic-featured.png',
  seo: {
    metaTitle: "Primary Keyword - Secondary Info | Ential",  // 50-60 chars
    metaDescription: "Compelling 150-160 character description with keyword and value prop.",
    keywords: ['primary keyword', 'secondary keyword', 'long-tail phrase'],  // 5-10
  },
  stats: [
    { label: 'Stat label', value: '123' },
  ],
  relatedSlugs: ['other-post-slug'],
  content: ({ isNightMode, setPage }) => (
    <>
      {/* Post content here */}
    </>
  )
}
```

### Step 2: Add to `views/Blog.tsx`

#### 2a. Add to ARTICLES array

**IMPORTANT:** The `image` property is REQUIRED. Use the same image path as `featuredImage` in blogPosts.tsx.

```tsx
{
  id: 'unique-id',
  title: 'Post Title Here',
  excerpt: 'Short excerpt for the listing page.',
  category: 'category-id',
  categoryLabel: 'Category Name',
  date: 'Dec 30, 2025',               // Short date format
  readTime: '6 min read',
  author: 'Ryan Drake',
  authorInitial: 'R',
  ticker: 'new',
  tickerText: 'Ticker text here',
  placeholder: '???',
  image: '/images/blog/topic-featured.png'  // REQUIRED - same as featuredImage in blogPosts.tsx
}
```

#### 2b. Add slug to navigation maps

Update BOTH slug maps in `views/Blog.tsx`:

```tsx
// Featured article click handler (~line 786)
const slugMap: Record<string, string> = {
  'linkedin-delete': 'i-deleted-2847-linkedin-messages-in-3-hours',
  'unique-id': 'seo-friendly-url-slug'  // ADD THIS
};

// Regular articles click handler (~line 853)
const slugMap: Record<string, string> = {
  'linkedin-delete': 'i-deleted-2847-linkedin-messages-in-3-hours',
  'unique-id': 'seo-friendly-url-slug'  // ADD THIS
};
```

#### 2c. Update category count

Increment the count for the relevant category in CATEGORIES array.

#### 2d. Update TRENDING array

When adding a new post, update the TRENDING array to include the latest posts:

**Rules:**
- **Maximum 4 posts** in the trending section
- **Newest post goes at the bottom** of the list (position 4)
- Remove the oldest post (position 1) if at max capacity
- Only include `id`, `title`, and `readTime` (no views)

```tsx
const TRENDING = [
  { id: 1, title: "Post Title One", readTime: '8 min read' },
  { id: 2, title: "Post Title Two", readTime: '6 min read' },
  { id: 3, title: "Post Title Three", readTime: '5 min read' },
  { id: 4, title: "Newest Post Title", readTime: '7 min read' }  // Latest at bottom
];
```

### Step 3: Add to `views/BlogPost.tsx` ticker

**REQUIRED:** Add the new post to the `tickerItems` array in BlogPost.tsx (~line 306):

```tsx
const tickerItems = [
  { tag: 'hot' as const, text: "Existing Hot Post Title" },
  { tag: 'new' as const, text: "Your New Post Title Here" },  // ADD THIS
  { tag: 'breaking' as const, text: "Existing Breaking Post" }
];
```

**Ticker types:**
- `'breaking'` - Major news/announcements
- `'hot'` - Popular or trending content
- `'new'` - Recently published content

### Step 4: Add to `route-metadata.ts` for SEO Pre-rendering

**CRITICAL FOR SEO:** Add the blog post to `routeMetadata` object for pre-rendering.

Find the `// BLOG POSTS` section (near line 345) and add:

```tsx
'/blog/your-post-slug': {
  path: '/blog/your-post-slug',
  title: "Post Title — Ential Blog",                          // 50-60 chars
  description: "Compelling meta description with keywords.",   // 150-160 chars
  keywords: 'keyword1, keyword2, keyword3, long-tail phrase',
  canonical: `${SITE_URL}/blog/your-post-slug`,
  ogTitle: "Post Title",
  ogDescription: "Short compelling description for social sharing.",
  ogImage: `${SITE_URL}/images/blog/your-image.png`,          // Optional: custom OG image
  ogType: 'article',
  priority: 0.8,
  changefreq: 'monthly',
},
```

**Why this matters:**
- Enables **pre-rendering** at build time (better SEO)
- Sets **canonical URLs** to prevent duplicate content
- Provides **Open Graph metadata** for social sharing
- Included in **sitemap** with correct priority

## Content Styling Guidelines

### Headings

**REQUIRED:** All h2 section headings must be amber colored:

```tsx
<h2 className="text-amber-500">Section Title</h2>
```

### Code Blocks

```tsx
<CodeBlock code="your code here" language="bash" isNightMode={isNightMode} />
```

**Compact mode:** Automatically applied for 1-5 lines.

### Images in Content

```tsx
<div className={`my-8 -mx-4 md:-mx-12 ${isNightMode ? 'bg-[#0d0d0d]' : 'bg-[#f5f2eb]'} p-4 md:p-8`}>
  <img
    src="/images/blog/topic-descriptor.png"
    alt="Descriptive alt text with keywords"
    className="w-full max-w-2xl mx-auto rounded-lg shadow-lg"
  />
  <p className={`text-center mt-4 font-mono text-xs ${isNightMode ? 'text-white/40' : 'text-[#6b6b6b]'}`}>
    Caption text here
  </p>
</div>
```

**Image alt text:** Must be descriptive and include relevant keywords for SEO.

## Human-Sounding Writing Rules

**CRITICAL:** All blog posts must follow these rules to sound human, not robotic. These rules are based on proven prompts that make AI content sound natural.

### Structure and Formatting
- Avoid separating topics with hyphens. Don't use the [topic] - [explanation] format.
- Write in flowing paragraphs like normal conversation.
- Use commas instead of hyphens to separate ideas.
- Only break paragraphs when actually changing subjects.

### Tone and Voice
- Maintain natural irregularity in sentence length. Alternate between short and long sentences.
- Sometimes be direct. Other times elaborate more, but don't force it.
- Avoid unnecessary metaphors and poetic comparisons for simple concepts.

### Conversational Behavior
- Disagree when it makes sense. Question incorrect premises.
- Don't automatically validate everything. If something is wrong, point it out naturally.
- Avoid starting responses with compliments about the user or the question.

### Specific Restrictions
- Never use emojis.
- Avoid caps lock completely.
- Don't use bold or italics to highlight words.
- Drastically limit the use of quotation marks for emphasis.
- Avoid bullet lists unless truly necessary.

### Language and Style
- Vary between formal and informal as context demands.
- Use contractions when appropriate.
- Avoid over-explaining your reasoning process.
- Don't announce what you're going to do before doing it.

### Content Guidelines
- Be specific rather than generic.
- Take positions when appropriate.
- Avoid always seeking artificial balance between viewpoints.
- Don't hesitate to be brief when the question is simple.
- Resist the temptation to always add extra context or elaborate unnecessarily.

### Words and Phrases to Avoid

**Never use these chatbot-typical phrases:**
- additionally, alternatively, amongst, arguably, as a professional, as previously mentioned, as well as, because, bridging, bustling, changing the game, compelling, consequently, crucial, cutting-edge, daunting, delve into, designed to enhance, dilemma, dive, dive into, diving, due to, embark, elevate, emphasize, ensure, essentially, essential, even though, ever-evolving, everchanging, evolving, excels, expand, expanding, fancy, fast, firstly, foster, foundations, furthermore, game changer, game-changing, generally, given that, gossamer, groundbreaking, harness, hey, imagine, immense, importantly, in conclusion, in contrast, in order to, in summary, in the quest, in the realm of, in the world of, in today's digital age, in today's digital era, indeed, indelible, intense, it is advisable, it's essential to, it's important to note, it's worth noting that, journey, keen, landscape, labyrinth, let's, mastering, metropolis, meticulous, meticulously, moreover, my friend, navigating, nestled, not only, notably, orchestrate, orchestrating, paced, picture this, paramount, power, pressure, profoundly, promptly, pursuit, quest, rapidly, realm, relentless, remember that..., remnant, reshape, reshaping, reverberate, revolutionize, robust, seismic, shall, sights unseen, sounds unheard, specifically, struggled, subsequently, take a dive into, tapestry, tailored, testament, the world of, there are a few considerations, thrilled, thus, to consider, to put it simply, to summarize, today's towards, transformative, ultimately, underpins, underscore, unleash, unlock the secrets, unprecedented, unveil the secrets, vibrant, vital, whispering, when it comes to, world, you may want to, understanding, alright, game changer, It is advisable.

**Avoid concepts like:**
- "In today's environment"
- "In today's business world"
- "Rapidly changing"
- "In the competitive business environment"
- "Being inclusive"

**Before publishing:** Review your content to ensure it adheres to these rules. The goal is to sound like a human wrote it, not a chatbot.

## Categories

| ID | Label | Description |
|----|-------|-------------|
| `everyday-ai` | Everyday AI | Practical AI tips and automation |
| `hub` | Marketing Hub | Marketing automation content |
| `inside-machine` | Inside The Machine | Technical deep dives |
| `founder-diaries` | Founder Diaries | Personal reflections |
| `blueprints` | Blueprints | Step-by-step guides |

## Ticker Types

| Type | Display |
|------|---------|
| `breaking` | Red pulsing "BREAKING" badge |
| `hot` | Amber "HOT" text |
| `new` | Amber "NEW" text |

---

## SEO Publishing Checklist (MANDATORY)

**Run this checklist before every publish. All items must pass.**

### Date Verification
- [ ] `date` is set to today's Brisbane date (format: `December 30, 2025`)
- [ ] `modifiedDate` matches `date` for new posts
- [ ] `date` in Blog.tsx uses abbreviated format (`Dec 30, 2025`)

### URL Slug SEO
- [ ] Slug is lowercase with hyphens only
- [ ] Slug is 3-8 words
- [ ] Slug contains primary keyword
- [ ] Slug is human-readable

### Image SEO (MANDATORY - Images Required)
- [ ] **Image file exists** in `public/images/blog/` directory
- [ ] All image files are lowercase with hyphens
- [ ] Image names are descriptive (no `IMG_`, `screenshot`, `image1`)
- [ ] Image names relate to post topic
- [ ] **`featuredImage` path is added** in blogPosts.tsx (required for individual post page)
- [ ] **`image` path is added** in Blog.tsx ARTICLES array (required for blog listing page)
- [ ] Both image paths use the same file path
- [ ] All `alt` attributes contain descriptive text with keywords

**REMINDER:** Images must be added to BOTH files or they will not display correctly.

### Meta Title SEO
- [ ] Length is 50-60 characters
- [ ] Contains primary keyword near beginning
- [ ] Ends with `| Ential`
- [ ] Is compelling and click-worthy

### Meta Description SEO
- [ ] Length is 150-160 characters
- [ ] Contains primary keyword
- [ ] Includes value proposition
- [ ] Has implicit or explicit call-to-action

### Keywords SEO
- [ ] Array contains 5-10 keywords
- [ ] Includes mix of short-tail and long-tail
- [ ] All keywords appear somewhere in content
- [ ] Keywords are lowercase

### Tags SEO
- [ ] Contains 3-5 tags
- [ ] Tags are Title Case
- [ ] Tags are specific (not generic like "Tech")
- [ ] No duplicate/redundant tags

### Content SEO
- [ ] H2 headings use `className="text-amber-500"`
- [ ] Content includes primary keyword in first paragraph
- [ ] Subheadings (h2, h3) include relevant keywords
- [ ] Internal links use `setPage()` navigation

### File Updates (ALL 4 FILES REQUIRED)
- [ ] Added to `data/blogPosts.tsx` (full post content)
- [ ] Added to `views/Blog.tsx` ARTICLES array
- [ ] Added to BOTH slug maps in Blog.tsx
- [ ] Updated TRENDING array (max 4, newest at bottom, only title + readTime)
- [ ] Category count updated
- [ ] **Added to `views/BlogPost.tsx` tickerItems array** (for news ticker)
- [ ] **Added to `route-metadata.ts`** (for SEO pre-rendering)

### SEO Pre-rendering (route-metadata.ts)
- [ ] Entry added to `routeMetadata` object under BLOG POSTS section
- [ ] `path` matches `/blog/your-slug`
- [ ] `title` is 50-60 chars, ends with "— Ential Blog"
- [ ] `description` is 150-160 chars with keywords
- [ ] `canonical` URL is set correctly
- [ ] `ogTitle` and `ogDescription` are compelling for social
- [ ] `ogType` is set to `'article'`
- [ ] `priority` is set to `0.8`

### Layout
- [ ] Featured image within 800px container
- [ ] Stats callout within 800px wrapper
- [ ] No full-width elements breaking layout

---

**If any SEO check fails, fix before publishing.**
