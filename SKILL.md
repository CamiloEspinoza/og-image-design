---
name: og-image-design
description: Design and generate Open Graph (OG) images for social media sharing. Use this skill whenever the user mentions OG images, social sharing images, social cards, Twitter cards, link preview images, meta images, og:image, social thumbnails, or wants to create images that appear when links are shared on Facebook, Twitter/X, LinkedIn, Discord, Slack, iMessage, or any social platform. Also use when the user asks about og:image meta tags, social preview optimization, or link unfurling visuals.
---

# OG Image Design

Design effective Open Graph images that make links stand out when shared across social platforms. This skill covers dimensions, layout, typography, color, HTML/CSS templates, and meta tag integration — independent of any specific image generation tool.

## Generation Approach

OG images are typically generated from HTML/CSS rendered to a static image. Choose whichever method fits the project:

| Method | When to use |
|---|---|
| **Next.js `ImageResponse`** (Satori + `@vercel/og`) | Next.js apps — generates at the edge, no browser needed |
| **Puppeteer / Playwright screenshot** | Any Node.js project — full browser rendering fidelity |
| **Satori standalone** | Lightweight JSX-to-SVG-to-PNG without a browser |
| **HTML-to-image CLI/API** | CI pipelines, serverless, or any language |
| **Static design tool export** | One-off images, manual workflow |
| **AI image generation** | Photographic or illustrative visuals without text layout concerns |

Regardless of method, the HTML/CSS templates and design rules below apply universally.

## Platform Specifications

| Platform | Dimensions | Aspect Ratio | Max Size | Formats |
|---|---|---|---|---|
| Facebook | 1200 × 630 px | 1.91:1 | 8 MB | JPG, PNG |
| Twitter/X (`summary_large_image`) | 1200 × 628 px | 1.91:1 | 5 MB | JPG, PNG, WEBP, GIF |
| Twitter/X (`summary`) | 800 × 418 px | 1.91:1 | 5 MB | JPG, PNG |
| LinkedIn | 1200 × 627 px | 1.91:1 | 5 MB | JPG, PNG |
| Discord | 1200 × 630 px | 1.91:1 | 8 MB | JPG, PNG |
| Slack | 1200 × 630 px | 1.91:1 | — | JPG, PNG |
| iMessage | 1200 × 630 px | 1.91:1 | — | JPG, PNG |

**Universal target: 1200 × 630 px, PNG or JPG, under 1 MB (under 5 MB absolute max).**

## The Golden Layout

```
┌──────────────────────────────────────────────────┐
│                                                  │
│  ┌─────────────────────────────────┐  ┌───────┐  │
│  │                                 │  │       │  │
│  │  Title (max 60 chars)           │  │ Logo/ │  │
│  │  ───────────────────            │  │ Visual│  │
│  │  Subtitle (max 100 chars)       │  │       │  │
│  │                                 │  │       │  │
│  │  author · site name             │  └───────┘  │
│  └─────────────────────────────────┘             │
│                                                  │
└──────────────────────────────────────────────────┘
  1200 × 630 px
```

This is the most reliable pattern: text-heavy left side, visual accent right side. Centered single-column layouts also work well for announcements and product launches.

## Design Rules

### Typography

| Property | Value |
|---|---|
| Title size | 48–64 px |
| Subtitle size | 20–28 px |
| Max title length | 60 characters (truncated on some platforms) |
| Max subtitle length | 100 characters |
| Line height | 1.2–1.3 for titles |
| Title weight | Bold or Black (700–900) |
| Subtitle weight | Regular (400) |
| Text contrast | WCAG AA minimum (4.5:1 ratio) |

Use `system-ui, -apple-system, "Segoe UI", sans-serif` as the base font stack for maximum compatibility. If the rendering engine supports custom fonts (Satori, Puppeteer), prefer Inter, Plus Jakarta Sans, or a brand font.

### Safe Zones

```
┌──────────────────────────────────────────────────┐
│  ┌──────────────────────────────────────────────┐│
│  │  40–60 px padding from all edges             ││
│  │                                              ││
│  │  Content lives here                          ││
│  │                                              ││
│  └──────────────────────────────────────────────┘│
└──────────────────────────────────────────────────┘
```

- 40 px minimum padding from all edges (60 px preferred).
- Some platforms crop edges or add rounded corners.
- Never place critical text in the outer 5%.

### Color & Background

| Background type | When to use |
|---|---|
| Solid brand color | Consistent series, corporate identity |
| Gradient | Modern feel, eye-catching |
| Photo with dark overlay | Blog posts, editorial content |
| Dark background | Better contrast, stands out in feeds |

Dark backgrounds outperform light ones in social feeds — most feeds have a light background, so dark OG images create contrast and draw the eye.

When using gradients, `135deg` diagonal gradients are a reliable default:

```css
background: linear-gradient(135deg, #1a1a2e, #16213e);
```

### Consistency System

For sites with many pages, keep these elements consistent across all OG images:

| Element | Keep consistent | Vary per page |
|---|---|---|
| Background style | Same gradient or brand palette | — |
| Font family | Same font stack | — |
| Layout | Same positioning template | — |
| Logo / branding | Same placement (e.g. bottom-left corner) | — |
| Category badge | Same style | Color per category |
| Title text | Same size and weight | Content changes |

## HTML/CSS Templates

These templates work with any HTML-to-image renderer. The outer `div` is always exactly `1200 × 630 px` with `display: flex`.

### Blog Post

```html
<div style="width:1200px;height:630px;background:linear-gradient(135deg,#667eea,#764ba2);display:flex;align-items:center;padding:60px;font-family:system-ui,sans-serif;color:white">
  <div style="flex:1">
    <p style="font-size:18px;text-transform:uppercase;letter-spacing:2px;opacity:0.8;margin:0">Engineering Blog</p>
    <h1 style="font-size:52px;margin:16px 0 0;line-height:1.2;font-weight:800">How We Reduced Build Times by 80%</h1>
    <p style="font-size:22px;opacity:0.9;margin-top:16px">A deep dive into CI/CD optimization</p>
  </div>
</div>
```

### Product / Launch Announcement

```html
<div style="width:1200px;height:630px;background:#0f0f0f;display:flex;align-items:center;justify-content:center;font-family:system-ui,sans-serif;color:white;text-align:center">
  <div>
    <p style="font-size:20px;color:#22c55e;text-transform:uppercase;letter-spacing:3px;margin:0">Now Available</p>
    <h1 style="font-size:64px;margin:12px 0;font-weight:900">ProductName 2.0</h1>
    <p style="font-size:24px;opacity:0.7;margin:0">Tagline goes here. Zero configuration.</p>
  </div>
</div>
```

### Tutorial / How-To

```html
<div style="width:1200px;height:630px;background:linear-gradient(to right,#1a1a2e,#16213e);display:flex;align-items:center;padding:60px;font-family:system-ui,sans-serif;color:white">
  <div>
    <div style="display:inline-block;background:#e74c3c;color:white;padding:8px 16px;border-radius:4px;font-size:16px;font-weight:bold;margin-bottom:16px">TUTORIAL</div>
    <h1 style="font-size:48px;margin:0;line-height:1.2">Build a REST API in 10 Minutes with Node.js</h1>
    <p style="font-size:20px;opacity:0.7;margin-top:16px">Step-by-step guide with code examples</p>
  </div>
</div>
```

### Documentation / Technical

```html
<div style="width:1200px;height:630px;background:linear-gradient(135deg,#0c0c0c,#1c1c1c);display:flex;align-items:center;padding:60px;font-family:system-ui,sans-serif;color:white">
  <div style="flex:1">
    <div style="display:flex;align-items:center;gap:12px;margin-bottom:24px">
      <div style="width:48px;height:48px;background:#3b82f6;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:24px;font-weight:900">D</div>
      <span style="font-size:20px;font-weight:600;opacity:0.8">Docs</span>
    </div>
    <h1 style="font-size:52px;margin:0;line-height:1.2;font-weight:800">Authentication API Reference</h1>
    <p style="font-size:22px;opacity:0.6;margin-top:16px">v2.0 — Updated March 2026</p>
  </div>
</div>
```

### Branded with Logo (right side)

```html
<div style="width:1200px;height:630px;background:linear-gradient(135deg,#0f172a,#1e293b);display:flex;align-items:center;padding:60px;font-family:system-ui,sans-serif;color:white">
  <div style="flex:1;padding-right:40px">
    <h1 style="font-size:52px;margin:0;line-height:1.2;font-weight:800">Your Title Goes Here</h1>
    <p style="font-size:22px;opacity:0.8;margin-top:16px">Supporting description text</p>
    <p style="font-size:18px;opacity:0.5;margin-top:24px">yoursite.com</p>
  </div>
  <div style="width:200px;height:200px;background:rgba(255,255,255,0.1);border-radius:24px;display:flex;align-items:center;justify-content:center;flex-shrink:0">
    <span style="font-size:64px;font-weight:900">☐</span>
  </div>
</div>
```

Replace the placeholder square with an `<img>` tag pointing to the actual logo when the renderer supports it.

## Adapting Templates

When customizing these templates:

1. **Replace placeholder text** with actual title, subtitle, and branding.
2. **Swap gradient colors** to match the brand palette. Keep at least two stops.
3. **Adjust font sizes** within the ranges (48–64 px title, 20–28 px subtitle). Longer titles need smaller sizes.
4. **Add a category badge** for content series — a small colored pill above the title.
5. **Truncate long text** rather than shrinking the font below minimum sizes. An ellipsis at 60 chars is better than 36 px text.

## OG Meta Tags Reference

```html
<!-- Essential (Facebook, LinkedIn, Discord, Slack, iMessage) -->
<meta property="og:title" content="Title here (60 chars max)" />
<meta property="og:description" content="Description (155 chars max)" />
<meta property="og:image" content="https://yoursite.com/og-image.png" />
<meta property="og:url" content="https://yoursite.com/page" />
<meta property="og:type" content="article" />

<!-- Recommended dimensions hint -->
<meta property="og:image:width" content="1200" />
<meta property="og:image:height" content="630" />

<!-- Twitter/X specific -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Title here" />
<meta name="twitter:description" content="Description" />
<meta name="twitter:image" content="https://yoursite.com/og-image.png" />
```

### Twitter Card Types

| Card type | Image size | Use when |
|---|---|---|
| `summary` | 800 × 418 (small thumbnail) | Short updates, links |
| `summary_large_image` | 1200 × 628 (full width) | Blog posts, articles, announcements |

Always prefer `summary_large_image` — the large image gets significantly more engagement.

### Next.js App Router Integration

In Next.js, OG images can be generated dynamically using route-level `opengraph-image.tsx` files or the `metadata` / `generateMetadata` API:

```tsx
// app/blog/[slug]/opengraph-image.tsx
import { ImageResponse } from "next/og";

export const runtime = "edge";
export const alt = "Blog post title";
export const size = { width: 1200, height: 630 };
export const contentType = "image/png";

export default async function Image({ params }: { params: { slug: string } }) {
  // Fetch post data, then return JSX that follows the design rules above
  return new ImageResponse(
    (
      <div style={{ width: "100%", height: "100%", display: "flex", alignItems: "center", padding: 60, background: "linear-gradient(135deg, #667eea, #764ba2)", fontFamily: "system-ui", color: "white" }}>
        <div style={{ display: "flex", flexDirection: "column" }}>
          <span style={{ fontSize: 52, fontWeight: 800, lineHeight: 1.2 }}>Post Title Here</span>
          <span style={{ fontSize: 22, opacity: 0.9, marginTop: 16 }}>Subtitle or description</span>
        </div>
      </div>
    ),
    { ...size }
  );
}
```

When using Satori (the engine behind `ImageResponse`), note that it supports a subset of CSS — `flexbox` layout works but `grid` does not. All elements must use `display: flex` and `flexDirection` for layout.

## Testing & Debugging

Validate OG images after deployment with these tools:

| Tool | URL |
|---|---|
| Facebook Sharing Debugger | `developers.facebook.com/tools/debug/` |
| Twitter/X Card Validator | `cards-dev.twitter.com/validator` |
| LinkedIn Post Inspector | `linkedin.com/post-inspector/` |
| OpenGraph.xyz | `opengraph.xyz` |

These tools fetch the URL, read the meta tags, and show a preview of how the link will appear when shared.

## Common Mistakes

| Mistake | Problem | Fix |
|---|---|---|
| No `og:image` at all | Platform shows random page element or blank | Always set `og:image` |
| Text too small | Unreadable on mobile previews | Title minimum 48 px at 1200 px width |
| Light background | Gets lost in white/light feeds | Use dark or saturated backgrounds |
| Too much text | Cluttered, overwhelming | Stick to title + subtitle + brand |
| Image too large (> 5 MB) | Some platforms won't load it | Optimize to under 1 MB ideally |
| No safe zone padding | Text gets cropped on some platforms | 40–60 px padding from all edges |
| HTTP image URL | Many platforms require HTTPS | Always serve OG images over HTTPS |
| Relative image path | Won't resolve when shared externally | Use full absolute URL with protocol |
| Missing `og:image:width` / `height` | Slower unfurling on some platforms | Always include dimension hints |
| Caching stale image | Updated image not reflected | Append version query param or use Facebook debugger to scrape again |
