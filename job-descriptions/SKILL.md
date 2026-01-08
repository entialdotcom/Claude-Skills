---
name: job-descriptions
description: Use this skill when creating, editing, or managing job descriptions for the Ential careers page. Handles job description structure, formatting, markdown rendering, URL routing, and file management. Ensures consistent styling with amber headlines, proper section ordering, and no redundant content.
allowed-tools: Read, Edit, Write, Glob, Grep
---

# Job Descriptions Editor

This skill provides comprehensive guidelines for creating and editing job descriptions for the Ential careers page, including proper structure, formatting, and URL routing.

## File Structure

Job descriptions are stored as markdown files in `public/jds/` and are dynamically loaded by the Careers page.

### File Locations

| File | Purpose |
|------|---------|
| `public/jds/*.md` | Job description markdown files (source of truth) |
| `utils/jobDescriptions.ts` | Utility functions to load and parse JD files, maps slugs to files |
| `components/JobDescriptionRenderer.tsx` | React component that renders markdown with proper formatting |
| `views/Careers.tsx` | Main careers page that displays job listings and details |
| `App.tsx` | Handles routing for individual job pages (`/careers/:slug`) |

## Job Description File Naming

Job description files MUST follow this naming pattern:

```
ai-[role-name]-upwork.md
```

Examples:
- `ai-automation-engineer-upwork.md`
- `ai-executive-assistant-upwork.md`
- `ai-graphic-designer-upwork.md`
- `ai-growth-marketer-upwork.md`
- `ai-customer-success-manager-upwork.md`

**Important:** The slug used in `utils/jobDescriptions.ts` determines the URL path. For example, `ai-automation-engineer` becomes `/careers/ai-automation-engineer`.

## Job Description Structure (CRITICAL ORDER)

Each job description markdown file MUST follow this exact structure and order:

```markdown
# [Job Title] — [Key Details] (Part-Time, Location)

[Brief intro paragraph describing the role]

---

## About Ential

[Company description - same for all roles]

## Role Overview

[2-3 sentence overview of the role, what makes it unique, and what the person will do]

## Why Join Us?

[Value proposition - why someone should want to work at Ential in this role. 
Should be compelling and specific to the role.]

## What You'll Do

- [Action-oriented bullet point]
- [Action-oriented bullet point]
- [Action-oriented bullet point]

## What We're Looking For

### Required Skills & Experience

- **[Bold requirement]** — [Description]
- **[Bold requirement]** — [Description]

### Bonus Experience (Highly Valued)

- **[Bold bonus]** — [Description]

### [Tool/Technology] Proficiency (Required)

[Description of tool requirements]

**Tools:**
- Tool 1 — [Usage]
- Tool 2 — [Usage]

### General AI Tool Proficiency (Required)

- **ChatGPT** — [Usage]
- **Claude** — [Usage]
- **Gemini** — [Usage]

### High Agency Mindset (Required)

We're looking for team members who take ownership, solve problems proactively, and don't wait for perfect conditions to take action.

**Before applying, read this article**: https://www.highagency.com/

We're looking for people who:
- Take initiative without waiting for permission
- Find creative solutions when obstacles appear
- Question assumptions and think from first principles
- Have a bias for action over endless planning
- Treat problems as solvable rather than accepting limitations

### Professional Remote Work Setup (Required)

To ensure productivity and professional standards, you must have:
- **Dedicated workspace** with professional setup (not working from bed or couch)
- **Dual monitor setup** minimum — laptop screen alone is not sufficient
- **High-speed internet**: Minimum 50 Mbps download / 10 Mbps upload
- **Typing speed**: Minimum [X] WPM with high accuracy
- **[Role-specific requirements]** (e.g., quality webcam, computer capable of video editing)

## Work Details

- **Type**: Part-time (X hours/week)
- **Hours**: [Schedule details]
- **Time Zone**: [Timezone requirements]
- **Reports to**: [Manager]
- **Communication**: [Communication method]

## How to Apply

⚠️ **IMPORTANT**: Incomplete applications will be automatically rejected. You must submit ALL of the following:

### 1. Application Keyword

Include the keyword **"[UNIQUE KEYWORD]"** in your application title or first line.

### 2. [Section Title]

[Content and instructions]

### 3. High Agency Reflection (150-200 words)

After reading https://www.highagency.com/, answer: "What does high agency mean to you, and how do you demonstrate it in your job/role?"

Share a specific example of when you took initiative, solved a problem creatively, or pushed through obstacles without waiting for permission.

### [N]. Workspace & Technical Verification

Submit verification of the remote work setup requirements listed above:
- **Photo of your workspace** showing your desk, dual monitor setup, and work environment
- **Typing speed test screenshot** (TypingTest.com or 10FastFingers.com — must show WPM and accuracy)
- **Internet speed test screenshot** (Fast.com or Speedtest.net — must show download/upload speeds)

### [N+1]. [Additional Application Requirements]

[More sections as needed]

---

**Applications missing any of the above requirements will not be considered.**

## ⛔ Critical Instruction

**Don't contact us outside of this official process and submitting below.**

Please submit your application correctly using the **"Apply For This Role"** button at the bottom of this page. This ensures your application is properly tracked and reviewed.

If you have questions, you can email us at careers@ential.com, but please use the application button for your initial submission.

This is a detail-oriented role. Following these application instructions is your first test.

---

**Skill Tags**: [Comma-separated list of relevant skills and keywords]
```

## Section Order Rules (MUST FOLLOW)

1. **Role Overview** - Always first after About Ential
2. **Why Join Us?** - Immediately after Role Overview
3. **What You'll Do** - After Why Join Us
4. **What We're Looking For** - After What You'll Do
   - High Agency and Professional Remote Work Setup go INSIDE this section
5. **Work Details** - After What We're Looking For
6. **How to Apply** - After Work Details
   - High Agency Reflection goes INSIDE this section (references the requirement above)
   - Workspace & Technical Verification is consolidated (not separate sections)
7. **Critical Instruction** - Always at the bottom

## Sections to AVOID (Redundant)

**DO NOT include these sections** - they are redundant and have been removed:

- ❌ "Screening Requirements Summary" - redundant with "What We're Looking For"
- ❌ Separate "Workspace Verification" and "Technical Verification" - use consolidated "Workspace & Technical Verification"
- ❌ Duplicate High Agency content in application section - reference the requirement instead

## Formatting Rules

### Headlines (CRITICAL)

**ALL section headings (H2, H3, H4) MUST use proper markdown syntax and will be automatically styled in amber:**

- H2 headings: `## Heading` (main sections)
- H3 headings: `### Heading` (subsections)
- H4 headings: `#### Heading` (sub-subsections)

The `JobDescriptionRenderer` component automatically applies amber styling (`text-amber-500` variants).

### No Emojis

**IMPORTANT:** The renderer automatically removes emojis from content. However, you should still avoid using emojis in the source markdown files for consistency.

**Exception:** The `⚠️` emoji in "Critical Instruction" and `⛔` in the section heading are preserved for emphasis.

### Bold Text

Use `**bold text**` for emphasis. The renderer will convert this to proper bold styling.

### Lists

- Use `- ` for unordered lists
- Lists are automatically styled with amber bullet points
- Proper spacing is applied automatically
- Numbered lists use `1. ` format and are styled with amber numbers

### Blockquotes

Use `> ` for blockquotes. These are styled with an amber left border.

### Code Blocks

Use triple backticks for code blocks:

````markdown
```language
code here
```
````

## URL Structure

Each job has its own unique URL based on the slug in `utils/jobDescriptions.ts`:

- `/careers/ai-automation-engineer`
- `/careers/ai-executive-assistant`
- `/careers/ai-graphic-designer`
- `/careers/ai-growth-marketer`
- `/careers/ai-customer-success-manager`

The "Back to Positions" link navigates to `/careers#positions` and automatically scrolls to the positions section.

## Updating Job Descriptions

### Step 1: Update the Markdown File

Edit the relevant file in `public/jds/`:

```bash
public/jds/ai-automation-engineer-upwork.md
```

**Ensure the section order matches the structure above.**

### Step 2: Update Job Metadata (if needed)

If you need to update job metadata (department, location, type, description, requirements), edit `utils/jobDescriptions.ts`:

```typescript
const jobFiles: Record<string, {...}> = {
  'ai-automation-engineer': {
    file: '/jds/ai-automation-engineer-upwork.md',
    dept: 'Engineering',
    remote: true,
    location: 'Remote (APAC)',
    type: 'Part-time',
    desc: 'Short description for listing page.',
    requirements: ['Skill1', 'Skill2', 'Skill3'],
  },
  // ... other jobs
};
```

**Note:** The key in `jobFiles` (e.g., `'ai-automation-engineer'`) determines the URL slug.

### Step 3: Verify Rendering

The `JobDescriptionRenderer` component automatically:
- Removes emojis (except ⚠️ and ⛔)
- Applies amber styling to headings
- Formats lists with amber bullets/numbers
- Handles bold text
- Renders code blocks
- Processes blockquotes
- Skips introductory paragraphs and "About Ential" section
- Removes "Skill Tags" section
- Creates callout boxes for "Critical" and "Important" sections

## Adding a New Job Description

### Step 1: Create Markdown File

Create a new file in `public/jds/` following the naming pattern:

```
public/jds/ai-[role-name]-upwork.md
```

**Follow the exact structure and section order outlined above.**

### Step 2: Add to `utils/jobDescriptions.ts`

Add the job to the `jobFiles` object:

```typescript
'new-job-slug': {
  file: '/jds/ai-new-role-upwork.md',
  dept: 'Department',
  remote: true,
  location: 'Remote (Location)',
  type: 'Part-time',
  desc: 'Short description for listing page (appears on careers listing).',
  requirements: ['Skill1', 'Skill2'],
},
```

**Important:** The key (`'new-job-slug'`) will become the URL path: `/careers/new-job-slug`

### Step 3: Verify

The job will automatically:
- Appear on the careers page listing
- Have its own URL at `/careers/[slug]`
- Be accessible via direct link

## Content Guidelines

### Section Content

#### Role Overview
- 2-3 sentences
- Focus on what makes the role unique
- Use engaging, action-oriented language
- Avoid generic descriptions

#### Why Join Us?
- Role-specific value proposition
- What makes working at Ential special for this role
- Growth opportunities, interesting challenges, cutting-edge work
- Should be compelling and authentic

#### What You'll Do
- Start each bullet with an action verb
- Be specific and measurable
- Focus on outcomes, not just tasks
- Use parallel structure
- 8-12 bullet points typically

#### What We're Looking For
- **Required Skills**: Must-have qualifications (be specific)
- **Bonus Experience**: Nice-to-have qualifications
- **Tool Proficiency**: List specific tools and how they're used
- **High Agency Mindset**: Standard text (copy from template)
- **Professional Remote Work Setup**: Standard format (adjust typing speed and role-specific requirements)

#### How to Apply
- Number all sections
- Be very specific about requirements
- Include unique application keyword
- High Agency Reflection references the requirement above (don't repeat full question)
- Workspace & Technical Verification is consolidated into one section

#### Critical Instruction
- Standard text (copy from template)
- Always at the bottom
- Email: careers@ential.com

### Headlines

- Use descriptive, action-oriented headlines
- Keep headlines concise (3-8 words)
- Use title case for section headings
- Avoid emojis in headlines (except ⛔ for Critical Instruction)

### Bullet Points

- Start with action verbs
- Be specific and measurable
- Focus on outcomes, not just tasks
- Use parallel structure
- Bold key terms when appropriate

### Required vs. Bonus

- **Required Skills**: Must-have qualifications (candidates without these won't be considered)
- **Bonus Experience**: Nice-to-have qualifications (differentiates candidates)
- Clearly distinguish between the two

### Application Instructions

- Be very specific about what's required
- Use clear formatting (numbered sections)
- Include unique application keywords (different for each role)
- Set clear expectations
- Reference requirements from earlier sections (don't repeat)

## Special Formatting Features

### Callout Boxes

The renderer automatically creates styled callout boxes for:

**Critical (Red theme):**
- Triggered by phrases like "Applications missing", "will not be considered", "automatically rejected"
- Red background, red border, red X icon

**Important (Amber theme):**
- Triggered by phrases like "IMPORTANT:", "must submit", "incomplete applications"
- Amber background, amber border, warning triangle icon

### Button Links

Links to `highagency.com` are automatically rendered as styled buttons.

### Content Filtering

The renderer automatically:
- Skips the introductory paragraph (before "Role Overview")
- Skips the "About Ential" section
- Skips the "Skill Tags" section at the bottom

## Styling Checklist

Before publishing a job description, verify:

- [ ] Section order matches the required structure exactly
- [ ] "Why Join Us?" is immediately after "Role Overview"
- [ ] High Agency and Professional Remote Work Setup are in "What We're Looking For"
- [ ] High Agency Reflection in "How to Apply" references the requirement (doesn't repeat full question)
- [ ] Workspace & Technical Verification is consolidated (not separate sections)
- [ ] No "Screening Requirements Summary" section
- [ ] Critical Instruction is at the bottom
- [ ] All H2 headings use `## ` syntax
- [ ] All H3 headings use `### ` syntax
- [ ] No emojis except ⚠️ and ⛔
- [ ] Bold text uses `**text**` syntax
- [ ] Lists use `- ` or `1. ` format
- [ ] Code blocks use triple backticks with language
- [ ] Blockquotes use `> ` format
- [ ] File name follows `ai-[role]-upwork.md` pattern
- [ ] Job metadata is added to `utils/jobDescriptions.ts`
- [ ] Slug in `jobDescriptions.ts` matches desired URL path
- [ ] Requirements array is populated with relevant skills
- [ ] Application keyword is unique for this role
- [ ] Email address is careers@ential.com (not .co)

## Common Issues

### Wrong Section Order

**Problem:** Sections are in the wrong order.

**Solution:** Follow the exact order specified in the structure above. Use the checklist to verify.

### Redundant Sections

**Problem:** "Screening Requirements Summary" or duplicate verification sections appear.

**Solution:** Remove these sections. They're redundant with "What We're Looking For" and the consolidated verification section.

### High Agency Content Duplicated

**Problem:** High Agency question is repeated in both requirements and application sections.

**Solution:** In "How to Apply", reference the requirement: "Answer the high agency question outlined in the requirements above."

### Headlines Not Amber

The `JobDescriptionRenderer` automatically applies amber styling. If headlines aren't amber, check:
1. Headings use proper markdown syntax (`## `, `### `, `#### `)
2. The renderer component is being used correctly

### URL Not Working

**Problem:** Job URL doesn't work or shows 404.

**Solution:**
1. Check that the slug in `utils/jobDescriptions.ts` matches the URL path
2. Verify the file exists in `public/jds/`
3. Check that routing is set up in `App.tsx` for `careers-job` page type

### "Back to Positions" Not Scrolling

**Problem:** Back button doesn't scroll to positions section.

**Solution:** The component automatically handles this. If it doesn't work, check that the `#positions` ID exists on the careers page.

---

## Quick Reference: Section Order

1. `#` Title
2. `---`
3. `## About Ential`
4. `## Role Overview`
5. `## Why Join Us?`
6. `## What You'll Do`
7. `## What We're Looking For`
   - `### Required Skills & Experience`
   - `### Bonus Experience`
   - `### [Tool] Proficiency`
   - `### General AI Tool Proficiency`
   - `### High Agency Mindset`
   - `### Professional Remote Work Setup`
8. `## Work Details`
9. `## How to Apply`
   - `### 1. Application Keyword`
   - `### 2. [Section]`
   - `### [N]. High Agency Reflection`
   - `### [N+1]. Workspace & Technical Verification`
   - `### [N+2]. [More sections]`
10. `---`
11. `## ⛔ Critical Instruction`
12. `---`
13. `**Skill Tags**: ...`

---

**Remember:** Job descriptions are the first impression candidates have of Ential. Make them clear, compelling, and professional. Follow the structure exactly to ensure consistency across all roles.
