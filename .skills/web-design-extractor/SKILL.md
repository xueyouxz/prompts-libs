---
name: web-design-extractor
description: "Analyze any live website and generate a detailed, reproducible design prompt. Use this skill whenever the user provides a website URL and wants to extract, deconstruct, or reverse-engineer its visual design, layout, interactions, or UI/UX patterns into a structured prompt. Triggers include: 'analyze this website', 'extract the design from this URL', 'generate a prompt from this site', 'deconstruct this page', 'reverse-engineer this website's design', 'how is this website designed', 'create a prompt to reproduce this site', or any request involving a URL combined with design analysis, prompt generation, or website cloning intent. Also triggers when users share a URL and ask to build something similar, replicate a layout, or study a site's design system. Works for single pages or multi-page analysis. Always use this skill even if the user just pastes a URL and says 'make something like this' — the extraction step is essential before any reproduction attempt."
---

# Web Design Extractor

Extract comprehensive, reproducible design prompts from live websites by systematically analyzing their DOM structure, visual styling, layout patterns, content hierarchy, interactions, and UX flows.

## When to Use

- User provides a URL and wants a design prompt generated from it
- User wants to clone, replicate, or build something inspired by a specific website
- User wants to study or deconstruct how a website is designed
- User shares multiple page URLs for multi-page analysis

## Core Workflow

Follow these steps in order. Do NOT skip steps — each builds on the previous.

### Step 1: Scope & Context Gathering

Ask the user (or infer from their message):

1. **Target URLs**: Which pages to analyze? Default = homepage only.
2. **Depth**: Full reproduction prompt vs. partial (e.g., just the color/type system, just the layout)?
3. **Output language**: Match the user's language for the prompt document.

Then use `web_search` to gather context about the site:
- What the company/product does
- Who built the site (agency, framework, CMS)
- Whether it's been featured on Awwwards, Dribbble, etc. (signals design quality)
- Tech stack clues (Next.js, Nuxt, GSAP, Framer Motion, etc.)

### Step 2: Fetch & Parse Each Page

For each target URL, use `web_fetch` to retrieve the full HTML. Then systematically extract:

**Read `references/analysis-framework.md` before proceeding.** It contains the complete checklist of what to analyze and how to describe each dimension.

Key extraction targets:

1. **Global chrome** — nav, footer, recurring elements
2. **Page sections** — identify every visually distinct block, top to bottom
3. **Content inventory** — exact headings, body text, CTAs, labels
4. **Image/media inventory** — count, aspect ratios, subjects, placement
5. **Layout patterns** — grid systems, breakpoints, asymmetry, whitespace
6. **Typography** — font families, sizes, weights, line-heights, letter-spacing
7. **Color system** — backgrounds, text, accents, gradients, opacity usage
8. **Interactive elements** — hover states, animations, transitions, scroll effects
9. **Component patterns** — cards, badges, buttons, forms, galleries, carousels

### Step 3: Cross-Page Synthesis (multi-page only)

When analyzing multiple pages:
- Extract the **shared design system** (nav, footer, colors, typography, spacing scale, button styles)
- Note what's **page-specific** vs. **global**
- Identify **navigation flow** and page transition patterns

### Step 4: Generate the Prompt Document

**Read `references/prompt-template.md` for the exact output structure.** The template defines the section order, heading levels, and formatting conventions.

Key principles for the output:

1. **Concrete over vague** — exact pixel sizes, color values, font names; never say "nice blue" when you can say "hsl(210 80% 55%)"
2. **Reproduce the actual content** — include real headings, paragraphs, button labels; don't summarize as "some text about X"
3. **Section-by-section** — describe the page in scroll order, top to bottom
4. **Developer-ready** — a developer reading this prompt should be able to build it without ever seeing the original
5. **Interaction details** — specify animation triggers, durations, easing, scroll behaviors
6. **Responsive notes** — mention how layouts change at breakpoints wherever observable

### Step 5: Output & Deliver

Save the prompt document as a `.md` file to `/mnt/user-data/outputs/` and present it to the user. For multi-page analyses, produce one unified document with clear page separators.

---

## Analysis Techniques

### Inferring What You Can't See

`web_fetch` returns rendered text content, not a visual screenshot. You must infer visual design from:

- **HTML structure**: tag nesting reveals layout hierarchy
- **Class names**: Tailwind classes (`flex`, `grid-cols-3`, `text-4xl`) directly encode styling; BEM/utility classes hint at component patterns
- **Inline styles**: sometimes carry key values
- **CSS variable names**: `--primary`, `--background`, etc. reveal the design token system
- **Image URLs and alt text**: reveal subjects, aspect ratios, and quantities
- **Content patterns**: repetition signals components (cards, list items)
- **Link structure**: reveals navigation hierarchy
- **Script references**: GSAP, Framer Motion, Three.js, Lenis, Locomotive Scroll signal animation approaches
- **Meta tags / schema**: reveal site purpose and technology

### Handling Limitations

- **SPAs / JS-heavy sites**: `web_fetch` may return minimal HTML. In this case, note the limitation and extract what you can from the text content, supplementing with `web_search` research.
- **CSS files**: If you find `<link>` tags pointing to CSS files, you can `web_fetch` those URLs to extract color variables, font imports, and keyframe definitions.
- **Fonts**: Look for Google Fonts links, `@font-face` declarations, or Typekit/Adobe Fonts references in the HTML.
- **Cannot see**: actual rendered layout, exact spacing measurements, animation timing, hover states. Use class names + conventions + experience to infer these.

### Framework Detection Cheatsheet

| Signal | Likely Stack |
|--------|-------------|
| `_next/`, `__next` | Next.js |
| `_nuxt/`, `__nuxt` | Nuxt.js |
| `wp-content/`, `wp-includes` | WordPress |
| `webflow.com` in scripts | Webflow |
| `framer.com` in scripts | Framer |
| `gsap`, `ScrollTrigger` | GSAP animation |
| `data-scroll`, `locomotive` | Locomotive Scroll |
| `lenis` | Lenis smooth scroll |
| `three`, `canvas`, `webgl` | Three.js / WebGL |
| `sanity.io` in image URLs | Sanity CMS |
| `contentful` | Contentful CMS |
| `prismic` | Prismic CMS |
| `shopify` | Shopify |

---

## Quality Checklist

Before delivering, verify the prompt covers ALL of these:

- [ ] Color system fully defined (background, foreground, primary, secondary, muted, border, accent — with HSL values)
- [ ] Typography fully defined (font families, size scale, weight scale, line-heights)
- [ ] Navigation described (desktop + mobile variants, fixed/sticky behavior)
- [ ] Footer described (layout, content, links)
- [ ] Every page section described in scroll order
- [ ] Actual text content included (headings, paragraphs, button labels)
- [ ] Image descriptions included (subject, count, aspect ratio, placement)
- [ ] Interactive behaviors noted (hover, scroll, click, animation)
- [ ] Responsive behavior noted where detectable
- [ ] Tech stack / framework identified
- [ ] Overall design tone/aesthetic characterized

---

## Reference Files

- `references/analysis-framework.md` — Detailed analysis dimensions and extraction checklist. **Read this before Step 2.**
- `references/prompt-template.md` — Output document structure and formatting conventions. **Read this before Step 4.**
