# Prompt Template

The output document structure for the extracted design prompt. Follow this format precisely — a developer reading this prompt should be able to reproduce the website without ever seeing the original.

---

## Document Structure

The prompt document is organized into these major sections, in this order:

```
1. Header & Metadata
2. Global Design System
3. Page-by-Page Sections (one per analyzed page)
4. Animation & Interaction Appendix
```

---

## 1. Header & Metadata

```markdown
# [Site Name] — 网站设计 Prompt

> 来源：[URL]
> 分析日期：[date]
> 技术栈：[framework, CMS, animation library, etc.]
> 设计风格：[2-3 word characterization, e.g., "极简奢华深色风" / "明亮SaaS扁平风"]
> 设计品质参考：[Awwwards 提名 / SOTD / 普通商业站等]
```

---

## 2. Global Design System

This section describes everything shared across ALL pages. Use code blocks for values, prose for relationships.

### 2.1 Color Theme

Always express as CSS custom properties with HSL values. Add a descriptive comment for each.

```markdown
### 颜色主题（使用 CSS 变量定义 HSL 值）

* --background: [H] [S]% [L]% ([description, e.g., 近纯黑])
* --foreground: [H] [S]% [L]% ([description])
* --primary: [H] [S]% [L]% ([description, e.g., 明亮青柠绿])
* --primary-foreground: [H] [S]% [L]% ([description])
* --secondary: [H] [S]% [L]% ([description])
* --secondary-foreground: [H] [S]% [L]% ([description])
* --muted: [H] [S]% [L]% ([description])
* --muted-foreground: [H] [S]% [L]% / [alpha] ([description])
* --border: [H] [S]% [L]% / [alpha] ([description])
* --accent: [H] [S]% [L]% ([description])
```

If the site uses gradients, note them separately:
```markdown
* 主渐变：from [color1] to [color2]，方向 [angle/direction]
```

### 2.2 Typography

```markdown
### 字体系统

* 标题/展示字体：[Font Name]（[serif/sans-serif/etc.]），用于 [where]
* 正文字体：[Font Name]（[serif/sans-serif/etc.]），用于 [where]
* 等宽字体：[Font Name]（如有），用于 [where]
* 字号层级：
  - 超大标题（Hero）：[size]px，[weight]，行高 [value]，字距 [value]
  - 区域标题（H2）：[size]px，[weight]，行高 [value]
  - 小标题（H3）：[size]px，[weight]
  - 正文：[size]px，[weight]，行高 [value]
  - 小号/辅助文字：[size]px，[weight]
  - 标签/徽章文字：[size]px，[weight]，大写/正常
* 响应式字号：
  - 超大标题：桌面 [size]px → 平板 [size]px → 手机 [size]px
```

### 2.3 Spacing Scale

```markdown
### 间距系统

* 页面最大宽度：[value]px
* 水平内边距：桌面 [value]px，平板 [value]px，手机 [value]px
* 区域间垂直间距：[value]px
* 组件内间距：[value]px
```

### 2.4 Navigation

Describe the nav in full detail, as it appears on every page.

```markdown
### 导航栏 (Navbar)

* 定位：[fixed/sticky/absolute]，[transparent/solid/blur]
* 背景：[description, including scroll-change behavior]
* 左侧：[brand element — text/logo, exact text if text, color details]
* 中间/右侧（桌面端）：[nav links — exact labels, styling]
* CTA 按钮（如有）：[label, color, shape, size]
* 移动端：[hamburger style, menu type — dropdown/overlay/drawer]
* 移动端菜单内容：[links, buttons, social, language switch]
* 动画：[open/close transition, link stagger, etc.]
```

### 2.5 Footer

```markdown
### 页脚 (Footer)

* 背景：[color/style]
* 布局：[column count, content per column]
* 第一列：[content]
* 第二列：[content]
* ...
* 底部行：[copyright, legal links]
* 文字样式：[font, size, color]
```

### 2.6 Global Components

If buttons, cards, badges, or other components appear across multiple pages, define their styles here once.

```markdown
### 按钮样式

* 主要按钮：[bg color], [text color], [border-radius], [padding], [font-size],
  [hover effect]
* 次要按钮：[same format]
* 幽灵按钮：[same format]

### 徽章/标签样式

* [shape], [border], [padding], [font-size], [color treatment]

### 卡片样式

* [border], [border-radius], [shadow], [background], [padding], [hover effect]
```

---

## 3. Page Sections

For each page, create a top-level heading. Within each page, describe every section in **scroll order** (top to bottom).

### Page heading format

```markdown
---

## 第 [N] 页：[Page Name]（[URL path]）

### 开发需求：[one-sentence summary of what to build]

[1-2 sentence design description: mood, layout approach, key visual strategy]
```

### Section description format

Each visible section on the page gets its own sub-section. Use this structure:

```markdown
### [Section Name] 区域

​```
* 高度/尺寸：[full-screen / auto / specific height]
* 背景：[color / image / video / gradient — with details]
* 布局：[layout pattern name + specifics]
  - [sub-layout details as needed]
* 内容元素（从上到下 / 从左到右）：
  a. [Element 1]：[exact text content] —— [styling: font, size, weight, color, alignment]
  b. [Element 2]：[exact text content] —— [styling]
  c. [Element 3]：[description] —— [styling]
* 图片/媒体：
  - [count] 张图片，[subject description]，[aspect ratio]，[treatment: rounded/circular/full-bleed]
  - [video if any: autoplay/loop/muted, URL or placeholder]
* 交互效果：
  - [hover behaviors]
  - [scroll-triggered animations]
  - [click behaviors]
* 响应式变化：
  - 平板：[changes]
  - 手机：[changes]
​```
```

### Content transcription rules

When transcribing text content:

1. **Include the full text** for short elements (headings, button labels, taglines, badge text, nav labels)
2. **Include the first 1-2 sentences** for long paragraphs, then summarize the rest
3. **Use exact text** — don't paraphrase headings or CTAs
4. **Note the language** if the site is multilingual
5. **Mark placeholder content** if text is clearly Lorem Ipsum or generic

### Image description rules

When describing images:

1. **Subject**: what the image shows (e.g., "现代别墅外观夜景照片" not "一张图片")
2. **Quantity**: "3 张并排" or "1 张全宽"
3. **Aspect ratio**: landscape 16:9, portrait 3:4, square 1:1, circular crop
4. **Treatment**: rounded corners (specify radius), circular, full-bleed, with overlay
5. **Purpose**: background, hero, product shot, decorative, avatar

---

## 4. Animation & Interaction Appendix

Collect all animation/interaction patterns into one reference section at the end.

```markdown
---

## 附录：动画与交互模式

### 页面过渡
* [type]: [duration], [easing]

### 滚动触发动画（ScrollTrigger / Intersection Observer）
* 图片入场：[from state] → [to state]，持续 [duration]，[easing]
* 文字入场：[animation type]，delay [stagger]
* 区域入场：[animation type]

### Hover 效果
* 文字链接：[effect]
* 按钮：[effect]
* 卡片：[effect]
* 图片：[effect]

### 特殊交互
* [Custom cursor / Parallax / Horizontal scroll / Marquee / etc.]

### 滚动行为
* [Smooth scroll library / native]
* [Any pinned sections / parallax layers]
```

---

## Formatting Rules

1. **Code blocks** (triple backtick) for structured property lists within sections
2. **Prose** for descriptions that need nuance and context
3. **Exact values** wherever possible — px, HSL, em, seconds
4. **Chinese** for structural labels and descriptions (matching the user's convention), English for technical terms and property names
5. **Consistent terminology** throughout:
   - 区域 = section
   - 布局 = layout
   - 字号 = font-size
   - 字重 = font-weight
   - 行高 = line-height
   - 字距 = letter-spacing
   - 内边距 = padding
   - 外边距 = margin
   - 圆角 = border-radius
   - 全圆角 = rounded-full / pill shape
6. **Use the pattern from the user's original template** wherever applicable — they provided a clear structure with backtick blocks, asterisk bullets, and em-dash separators for styling notes

---

## Example Section (for reference)

```markdown
### Hero 区域

​```
* 高度：全视口高度（h-screen）
* 背景：全屏建筑摄影图片轮播（7 张高品质建筑/别墅照片）
  - 图片使用 object-cover 覆盖整个区域
  - 轮播方式：自动交叉淡入淡出，约 5 秒切换
  - 带有 GSAP 缩放动画（Ken Burns 效果，scale 1.0 → 1.05，持续 5s）
* 遮罩：底部 30% 区域有从透明到 rgba(0,0,0,0.6) 的渐变遮罩
* 内容布局：品牌名居中
  - 品牌名 "ARCHIDOMO" —— 衬线体，100px，全大写，字距 0.15em，白色
  - 位置：垂直水平居中
* 底部：滚动指示器（细线动画，高 60px，白色，opacity 0.6）
* 交互：首次加载时品牌名从 opacity:0 + scale:0.95 淡入，持续 1.2s，ease-out
​```
```

---

## Multi-Page Document Layout

When analyzing multiple pages, use this structure:

```markdown
# [Site Name] — 网站设计 Prompt

> [metadata block]

## 全局设计系统（所有页面共用）
### 颜色主题
### 字体系统
### 间距系统
### 导航栏
### 页脚
### 全局组件样式

---

## 第 1 页：首页 (/)
### 开发需求：...
### Hero 区域
### [Section 2]
### [Section 3]
...

---

## 第 2 页：[Page Name] (/path)
### 开发需求：...
### [sections...]

---

## 第 N 页：...

---

## 附录：动画与交互模式
```

Each page gets its own `---` separator and numbered heading. Shared elements (nav, footer) are defined once in the Global Design System and not repeated per page.
