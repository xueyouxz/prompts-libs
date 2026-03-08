# Analysis Framework

A systematic checklist for deconstructing every design dimension of a web page. Work through each section for every page analyzed.

---

## 1. Site-Level Context

Before diving into visual details, establish:

- **Purpose**: What does this site/company do? Who is the target audience?
- **Brand tone**: Luxury? Playful? Corporate? Minimal? Brutalist? Editorial?
- **Design era/style**: Is this a modern GSAP-heavy portfolio site? A clean SaaS landing page? A bold editorial layout?
- **Tech stack**: Framework, CMS, animation library, hosting. Use the detection cheatsheet in SKILL.md.
- **Design quality**: Is this an award-winning site? Simple template? Custom build?

Capture this as 2-3 sentences at the top of the output — it frames everything that follows.

---

## 2. Color System

Extract a complete color token set. Express all values in HSL for readability, with descriptive names.

### What to extract

| Token | What it controls | Where to look |
|-------|-----------------|---------------|
| `--background` | Page/section backgrounds | `<body>`, `<main>`, section containers |
| `--foreground` | Primary text color | `<p>`, `<h1>`-`<h6>`, body text |
| `--primary` | Brand accent / CTA color | Buttons, links, highlighted elements |
| `--primary-foreground` | Text on primary-colored surfaces | Button text, badge text |
| `--secondary` | Secondary action color | Secondary buttons, alternate accents |
| `--secondary-foreground` | Text on secondary surfaces | Secondary button text |
| `--muted` | Subtle background tones | Card backgrounds, divider areas |
| `--muted-foreground` | De-emphasized text | Captions, metadata, placeholders |
| `--border` | Borders and dividers | Card borders, section dividers, input borders |
| `--accent` | Hover/focus/highlight states | Hover backgrounds, focus rings |
| `--destructive` | Error/danger states (if present) | Error messages, delete buttons |

### How to extract

1. Look for CSS custom properties in `<style>` tags or inline styles: `--background`, `--primary`, etc.
2. Look for Tailwind config values in class names: `bg-zinc-950`, `text-emerald-400` encode specific colors.
3. Look at explicit color values: `background-color: #0a0a0a`, `color: rgba(255,255,255,0.8)`.
4. If no explicit values found, infer from the site's visual description and context (dark site = near-black background, etc.).
5. Note opacity/alpha usage — many modern sites use semi-transparent whites/blacks for layering.

### Color relationship analysis

- Is this a **dark mode** or **light mode** site (or both)?
- How many distinct colors are used? (minimal = 2-3, rich = 5-8)
- Are colors **flat** or do they use **gradients**? Note gradient directions and stops.
- Is there a **monochromatic** scheme, **complementary**, **analogous**, etc.?

---

## 3. Typography System

### Font families

Look for these sources:
- Google Fonts: `<link href="https://fonts.googleapis.com/css2?family=..."`
- Adobe Fonts / Typekit: `use.typekit.net`
- Self-hosted: `@font-face` in `<style>` blocks
- CSS declarations: `font-family: "Playfair Display", serif`
- Class names: `font-serif`, `font-mono`, `font-display`

Identify:
- **Display/heading font**: usually a distinctive serif, slab, or decorative face
- **Body font**: usually a clean sans-serif
- **Monospace font** (if used): for code blocks, data, technical content
- **Accent font** (if different from above): sometimes used for pull quotes, labels

### Size scale

Map the heading hierarchy:
```
h1 / hero title: [size]px, [weight], [line-height], [letter-spacing]
h2 / section title: ...
h3 / subsection: ...
h4 / card title: ...
Body text: ...
Small / caption: ...
Label / tag: ...
```

Extract from:
- HTML tag sizes (`<h1>` vs `<p>`)
- Class names: `text-7xl` = ~72px, `text-5xl` = ~48px, `text-lg` = ~18px
- Inline styles: `font-size: 62px`

### Weight & style

- Note which elements are light (300), regular (400), medium (500), semibold (600), bold (700)
- Note italic usage, uppercase transforms (`uppercase`, `text-transform`)
- Note letter-spacing: tight, normal, wide, extra-wide

### Responsive typography

If detectable (e.g., `md:text-5xl lg:text-7xl`), note size changes at breakpoints.

---

## 4. Layout System

### Page-level layout

- **Max width**: is content constrained (`max-w-7xl` = 1280px) or full-bleed?
- **Horizontal padding**: consistent gutters (e.g., `px-6 lg:px-20`)?
- **Section spacing**: vertical gaps between major sections (e.g., `py-24`, `py-32`)

### Grid patterns

For each section, identify:
- **Column count**: 1, 2, 3, 4, or asymmetric (e.g., 2/3 + 1/3)
- **Gap size**: between grid items
- **Alignment**: items start-aligned, centered, or end-aligned
- **Responsive behavior**: how columns collapse (e.g., 3-col → 1-col on mobile)

### Common layout archetypes

Identify which patterns appear:

| Pattern | Description |
|---------|-------------|
| **Hero full-bleed** | Full-viewport-height section with background image/video |
| **Split hero** | Two-column: text left, image right (or reversed) |
| **Centered stack** | Centered text with constrained max-width |
| **Bento grid** | Mixed-size cards in a grid (like Apple's feature pages) |
| **Alternating zigzag** | Image-text pairs that alternate left/right |
| **Horizontal scroll** | Content moves horizontally on vertical scroll |
| **Masonry** | Pinterest-style irregular grid |
| **Sticky sidebar** | Content scrolls while a panel stays fixed |
| **Full-screen sections** | Each section = one viewport height |
| **Overlap/layered** | Elements overlapping or bleeding across sections |
| **Asymmetric composition** | Intentionally off-center or unbalanced |

### Whitespace analysis

- Is the design **dense** (tight spacing, lots of content) or **airy** (generous negative space)?
- Where is whitespace used strategically (around headlines, between sections)?
- Note specific spacing values if detectable from classes

---

## 5. Navigation & Chrome

### Primary navigation

- **Type**: horizontal bar, vertical sidebar, hamburger-only, full-screen overlay, off-canvas
- **Position**: fixed top, sticky, absolute, relative
- **Background**: solid, transparent, blur/glass, gradient, changes on scroll
- **Brand/logo**: text, image, or icon? Position? Size?
- **Link items**: exact labels, count, styling (font, size, weight, color, spacing)
- **Active state**: how the current page is indicated
- **CTA button**: label, color, shape, position
- **Mobile behavior**: hamburger icon style, dropdown vs overlay vs drawer, animation

### Footer

- **Layout**: column count, content in each column
- **Content**: nav links, contact info, social links, newsletter form, legal text
- **Visual style**: same background as page? Darker? Different texture?
- **Separators**: lines, spacing, or nothing between sections

---

## 6. Component Inventory

For each unique component type found on the page:

### Buttons

- **Primary**: background color, text color, border-radius, padding, font size, hover effect
- **Secondary**: same dimensions but different color treatment
- **Ghost/outline**: border-only variant
- **Icon buttons**: with leading/trailing icons
- **Sizes**: small, default, large

### Cards

- **Structure**: image position (top, side, background), title, description, metadata, CTA
- **Dimensions**: aspect ratio, max-width
- **Border**: none, subtle, prominent
- **Background**: solid, transparent, gradient
- **Shadow**: none, subtle, elevated
- **Border-radius**: sharp (0), slight (4-8px), rounded (12-16px), pill (full)
- **Hover effect**: scale, shadow, overlay, border color change

### Badges / Tags / Pills

- **Shape**: rounded-full, rounded, square
- **Size**: text size, padding
- **Color**: filled, outline, subtle background
- **Content**: text only, icon + text

### Forms & Inputs

- **Style**: bordered box, underline-only, filled background
- **Border-radius**: matches button style?
- **Focus state**: border color, ring, glow
- **Labels**: above, inside (floating), beside

### Image treatments

- **Border-radius**: square, rounded, circular
- **Aspect ratios**: 16:9, 4:3, 1:1, 3:4, free-form
- **Object-fit**: cover, contain, fill
- **Overlays**: dark gradient, color tint, blur
- **Hover effects**: zoom, opacity, overlay reveal

---

## 7. Interaction & Animation

### Scroll-triggered animations

- **Entry animations**: fade-in, slide-up, scale-in, clip-path reveal
- **Stagger**: do items animate in sequence?
- **Trigger point**: when does the animation start (element enters viewport)?
- **Duration**: fast (0.3s), medium (0.6s), slow (1s+)?
- **Easing**: ease-out, ease-in-out, spring, custom cubic-bezier

### Hover states

- **Text links**: underline appears, color change, background highlight
- **Buttons**: brightness/saturation change, scale, shadow
- **Cards**: elevation change, border highlight, image zoom
- **Images**: zoom, overlay, caption reveal

### Page transitions

- **Type**: instant, fade, slide, morph, shared-element
- **Duration**: estimated timing

### Scroll behavior

- **Smooth scroll**: Lenis, Locomotive, native smooth-scroll
- **Parallax**: background images move at different speeds
- **Pinned sections**: sections that stick while content scrolls within
- **Progress indicators**: scroll progress bars, section indicators
- **Horizontal scroll**: vertical scrolling drives horizontal movement

### Micro-interactions

- **Custom cursor**: modified cursor on hover over certain elements
- **Magnetic elements**: buttons/links that attract toward cursor
- **Text splitting**: characters or words animate independently
- **Counter/number animations**: numbers count up when visible
- **Marquee / infinite scroll**: text or images scroll continuously

### Loading & state transitions

- **Page loader**: preloader screen, progress bar, skeleton
- **Image loading**: blur-up, fade-in, placeholder color
- **Lazy loading**: images load as they enter viewport

---

## 8. Content Architecture

### Information hierarchy

For each section, map:
1. **Primary message**: the one thing the user should take away
2. **Supporting content**: elaboration, details, proof
3. **Action**: what the user should do next (CTA)

### Content types

- **Editorial/narrative**: long-form prose, storytelling
- **Feature grid**: multiple features with icon + title + description
- **Testimonial/social proof**: quotes, logos, ratings
- **Pricing table**: plan comparison
- **FAQ**: question/answer pairs
- **Portfolio/gallery**: project showcases
- **Team**: member cards with photos and bios
- **Timeline**: chronological events
- **Statistics/metrics**: big numbers with labels
- **Map/locations**: physical presence

### Media content

For each image or video:
- **Subject**: what does it depict?
- **Quantity**: how many in this section?
- **Aspect ratio**: landscape, portrait, square
- **Treatment**: full-bleed, contained, rounded, circular crop
- **Purpose**: hero background, product shot, decorative, informational

---

## 9. Responsive Behavior

Note detectable breakpoint changes:
- **Desktop** (>1024px): full layout
- **Tablet** (768-1024px): what changes?
- **Mobile** (<768px): what changes?

Common responsive patterns to identify:
- Multi-column → single-column stacking
- Horizontal nav → hamburger menu
- Font size reductions
- Hidden elements on mobile
- Full-width images on mobile
- Reduced padding/margins

---

## 10. Special / Differentiating Features

What makes this site unique or memorable?

- **Custom cursor** effects
- **3D / WebGL** elements
- **Video** backgrounds or integrated video
- **Sound** design
- **Dynamic data** visualization
- **Personalization** or interactive configuration
- **Unusual scrolling** mechanics
- **Split-screen** designs
- **Dark/light mode** toggle
- **Accessibility** features (skip links, ARIA, reduced motion)
- **Internationalization** (language switcher, RTL support)
- **Cookie consent** banner style
- **404 page** design
