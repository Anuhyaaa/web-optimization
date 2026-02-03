# 🚀 CAP785: Web Performance Optimization - Complete Guide

> **A comprehensive, beginner-friendly guide to making websites faster. Every concept is explained in simple language.**

---

## Table of Contents

1. [Unit I: Understanding & Assessing Web Performance](#unit-i-understanding--assessing-web-performance)
2. [Unit II: CSS Optimization & Critical CSS](#unit-ii-css-optimization--critical-css)
3. [Unit III: Image Optimization](#unit-iii-image-optimization)
4. [Unit IV: Fonts & JavaScript Optimization](#unit-iv-fonts--javascript-optimization)
5. [Unit V: Service Workers & Asset Delivery](#unit-v-service-workers--asset-delivery)
6. [Unit VI: HTTP/2 & Gulp Automation](#unit-vi-http2--gulp-automation)
7. [Practicals](#practicals)

---

## Course Outcomes

| CO | Description |
|----|-------------|
| **CO1** | Understand how to increase web performance using various techniques |
| **CO2** | Analyze websites for higher conversions and better user satisfaction |
| **CO3** | Evaluate the performance of web resources using various metrics |
| **CO4** | Construct websites for better user engagement and ranking |

---

# Unit I: Understanding & Assessing Web Performance

## 1.1 Introduction to Web Performance

### What is Web Performance?

**Web performance** refers to how quickly a website loads and becomes usable. Think of it like a restaurant - customers don't like waiting too long for their food, and website visitors don't like waiting for pages to load.

> **Simple Definition:** Web performance is the speed at which your website downloads, displays content, and responds to user actions.

### Why Does Web Performance Matter?

#### 1. User Experience

- **53% of mobile users** leave a website if it takes more than 3 seconds to load
- Slow websites feel frustrating and unprofessional
- Fast websites feel modern and trustworthy

#### 2. Business Impact

- **Amazon** found that every 100ms delay cost them 1% in sales
- **Google** discovered that a 0.5 second delay caused 20% drop in traffic
- Fast websites have higher **conversion rates** (visitors becoming customers)

#### 3. SEO (Search Engine Optimization)

- **Google uses page speed as a ranking factor**
- Slower websites rank lower in search results
- Core Web Vitals are now part of Google's ranking algorithm

### Understanding Key Performance Terms

Let's break down all the important terms you'll encounter:

---

## 1.2 Performance Metrics Explained (In Simple Language)

### Loading Metrics - How Fast Content Appears

#### TTFB (Time to First Byte)
>
> **What it means:** How long it takes for the server to send the first piece of data to your browser.

**Analogy:** Imagine ordering food at a restaurant. TTFB is like seeing the waiter walk toward your table - you know food is coming, but haven't seen it yet.

**Good TTFB:** Less than 800 milliseconds (0.8 seconds)

**What affects TTFB:**

- Server processing speed
- Database queries
- Network distance between user and server

---

#### FCP (First Contentful Paint)
>
> **What it means:** When the first text, image, or visible element appears on screen.

**Analogy:** It's like seeing the menu placed on your table - now you know the restaurant is actually working on serving you.

**Good FCP:** Less than 1.8 seconds

**What it measures:**

- When the user sees *something* on the page
- Does NOT mean the page is fully loaded
- First sign of progress for the user

---

#### LCP (Largest Contentful Paint) ⭐ Core Web Vital
>
> **What it means:** When the biggest visible element (usually hero image or main heading) finishes loading.

**Analogy:** When the main course arrives at your table - the most important part of your order is now visible.

**Why it matters:**

- This is what users perceive as "the page has loaded"
- Google uses this as a Core Web Vital (affects SEO)

| LCP Score | Rating |
|-----------|--------|
| ≤ 2.5 seconds | 🟢 Good |
| 2.5 - 4 seconds | 🟡 Needs Improvement |
| > 4 seconds | 🔴 Poor |

**What typically causes LCP:**

- Hero images
- Large text blocks
- Video poster images
- Background images

---

### Interactivity Metrics - How Responsive the Page Feels

#### FID (First Input Delay)
>
> **What it means:** How long the browser takes to respond to your FIRST click, tap, or keypress.

**Analogy:** You press a button on a remote control - FID measures how long until the TV actually responds.

**Good FID:** Less than 100 milliseconds

**Why delays happen:**

- Browser is busy loading/running JavaScript
- Main thread is blocked by heavy computations
- Too many scripts running at once

---

#### INP (Interaction to Next Paint) ⭐ Core Web Vital (Replaced FID in 2024)
>
> **What it means:** Measures responsiveness throughout the ENTIRE page visit, not just the first click.

**Simple explanation:** While FID only measures your first interaction, INP measures ALL your interactions and reports the worst one.

| INP Score | Rating |
|-----------|--------|
| ≤ 200 milliseconds | 🟢 Good |
| 200 - 500 milliseconds | 🟡 Needs Improvement |
| > 500 milliseconds | 🔴 Poor |

**Why INP replaced FID:**

- More accurate representation of user experience
- FID only measured first interaction, missing later problems
- INP captures the complete picture

---

#### TBT (Total Blocking Time)
>
> **What it means:** The total time during page load when the browser couldn't respond to user input.

**Analogy:** Imagine a customer service line where you're put on hold. TBT is the total time you spent on hold while the page was loading.

**Technical explanation:**

- Browser has a "main thread" that handles user interactions
- When JavaScript runs, it "blocks" this thread
- Any task longer than 50ms is considered "long" and blocks interactions
- TBT = Sum of all time beyond 50ms for each long task

**Example:**

```
Task 1: 30ms  → Not long (under 50ms), adds 0ms to TBT
Task 2: 150ms → Long task! Adds 100ms to TBT (150-50=100)
Task 3: 75ms  → Long task! Adds 25ms to TBT (75-50=25)

Total TBT = 0 + 100 + 25 = 125ms
```

**Good TBT:** Less than 200 milliseconds

---

### Visual Stability Metrics

#### CLS (Cumulative Layout Shift) ⭐ Core Web Vital
>
> **What it means:** Measures how much page content jumps around unexpectedly while loading.

**Analogy:** You're about to click a button, but suddenly an ad loads above it, pushing the button down. You accidentally click the ad instead. That's a layout shift!

**Why it's frustrating:**

- You click the wrong thing
- Hard to read jumping text
- Makes the site feel broken

| CLS Score | Rating |
|-----------|--------|
| ≤ 0.1 | 🟢 Good |
| 0.1 - 0.25 | 🟡 Needs Improvement |
| > 0.25 | 🔴 Poor |

**Common causes of layout shifts:**

- Images without width/height specified
- Ads that load later
- Fonts that swap after loading
- Dynamic content inserted above existing content

**How to prevent CLS:**

- Always set width and height on images
- Reserve space for ads
- Use font-display: swap with fallback fonts

---

### Custom/Additional Metrics

#### TTI (Time to Interactive)
>
> **What it means:** When the page is fully loaded AND can reliably respond to user input.

**Analogy:** The restaurant is open, staff is ready, and they can take your order immediately without delay.

**The difference from other metrics:**

- FCP = Something is visible
- LCP = Main content is visible
- TTI = Everything is ready and responsive

---

#### Speed Index
>
> **What it means:** How quickly the visible parts of the page are displayed.

**Technical definition:** Average time at which visible parts of the page are displayed.

**Analogy:** If a page loads in pieces over 5 seconds, Speed Index considers HOW those pieces load. A page showing 80% content at 1 second has a better Speed Index than one showing 20% at 1 second.

**Good Speed Index:** Less than 3.4 seconds

---

## 1.3 The Three Pillars of Web Performance

Web performance can be divided into three main categories:

### 1. Loading Performance

**Definition:** How fast content downloads and appears

**Key Questions:**

- How big are your files?
- How fast is your server?
- How far is the user from your server?

**Metrics:** TTFB, FCP, LCP, Speed Index

---

### 2. Rendering Performance

**Definition:** How smoothly the page displays and animates

**Key Questions:**

- Does scrolling feel smooth?
- Do animations run at 60fps?
- Does the page feel "janky" or smooth?

**Target:** 60 frames per second (16.67ms per frame)

---

### 3. Interactivity

**Definition:** How quickly the page responds to user actions

**Key Questions:**

- Does clicking feel instant?
- Is there delay when typing?
- Do buttons respond immediately?

**Metrics:** FID, INP, TBT, TTI

---

## 1.4 Understanding How Browsers Load Pages

To optimize performance, you need to understand what happens when someone visits your website:

### The Browser Loading Process

```
User types URL and presses Enter
           ↓
1. DNS Lookup
   Browser asks: "What's the IP address for this domain?"
   (Like looking up a phone number in a directory)
           ↓
2. TCP Connection
   Browser connects to the server
   (Like dialing the phone number)
           ↓
3. TLS/SSL Handshake (for HTTPS)
   Browser and server establish secure connection
   (Like verifying you're talking to the right person)
           ↓
4. HTTP Request
   Browser asks: "Send me the HTML for this page"
           ↓
5. Server Response (TTFB measured here)
   Server sends back HTML
           ↓
6. HTML Parsing
   Browser reads HTML and builds DOM
   (Document Object Model - the page structure)
           ↓
7. Discover Resources
   Browser finds CSS, JavaScript, images in HTML
           ↓
8. Download Resources
   Browser downloads CSS, JS, images in parallel
           ↓
9. Execute JavaScript
   Browser runs your scripts
           ↓
10. Render Page
    Browser paints pixels on screen
    (FCP happens here)
           ↓
11. Page Interactive
    User can interact with the page
    (TTI measured here)
```

### Critical Rendering Path

**Definition:** The sequence of steps the browser takes to convert HTML, CSS, and JavaScript into pixels on the screen.

**Why it matters:** The faster this path completes, the faster users see your content.

**The steps:**

1. **Build DOM** (from HTML)
2. **Build CSSOM** (from CSS) - BLOCKS rendering!
3. **Build Render Tree** (combine DOM + CSSOM)
4. **Layout** (calculate positions)
5. **Paint** (draw pixels)

> **Key insight:** CSS blocks rendering. The browser won't show anything until CSS is downloaded and processed. This is why "critical CSS" matters (covered in Unit II).

---

## 1.5 Assessment Tools

### Google PageSpeed Insights

**What it is:** A free tool from Google that analyzes your webpage and gives performance scores.

**URL:** <https://pagespeed.web.dev>

**What it provides:**

- Performance score (0-100)
- Core Web Vitals readings
- Specific recommendations for improvement
- Both mobile and desktop analysis

**Two types of data:**

1. **Field Data** (Real-world) - Actual data from Chrome users visiting your site
2. **Lab Data** (Simulated) - Tests run by Google's servers right now

---

### Chrome DevTools

**What it is:** Built-in developer tools in Chrome browser.

**How to open:** Press F12 or right-click → "Inspect"

**Key panels for performance:**

#### Network Panel

Shows all files downloaded when loading a page:

- File sizes
- Download times
- Request order
- Blocked time

#### Performance Panel

Records detailed timeline of page loading:

- CPU usage
- Screenshot timeline
- Main thread activity
- Long tasks

#### Lighthouse Panel

Runs automated audits:

- Performance
- Accessibility
- Best Practices
- SEO

#### Coverage Panel

Shows unused CSS and JavaScript:

- Red = unused code
- Green = used code
- Helps identify code to remove

---

### Network Request Inspection

When analyzing network requests, pay attention to:

| Column | What to Look For |
|--------|------------------|
| **Status** | 200=OK, 404=Not Found, 500=Server Error |
| **Size** | Files over 100KB need attention |
| **Time** | Slow files that delay page load |
| **Initiator** | What triggered this download |
| **Waterfall** | Visual timeline of download |

---

### Understanding the Waterfall Chart

The waterfall shows how resources load over time:

```
File             Time →
─────────────────────────────────────────
index.html       ▓▓░░░░░░░░░░░░░░░░░░░░░░
styles.css          ▓▓▓▓▓▓░░░░░░░░░░░░░░░
app.js                    ▓▓▓▓▓▓▓▓▓░░░░░░
hero.jpg                        ▓▓▓▓▓▓▓▓▓
font.woff2                           ▓▓▓▓

Legend: ▓ = downloading, ░ = waiting
```

**Reading the waterfall:**

- Vertical lines show when files start downloading
- Longer bars = bigger files or slower downloads
- Gaps = waiting time (potential optimization opportunity)

---

## 1.6 Network Throttling and Device Simulation

### Why Simulate Slower Conditions?

**The problem:** Developers usually have fast computers and fast internet. But users don't!

**Reality check:**

- Average mobile phone is 4-6x slower than developer's laptop
- Many users have 3G or slow 4G connections
- Not everyone lives near data centers

### Chrome DevTools Throttling

**How to enable:**

1. Open DevTools (F12)
2. Go to Network tab
3. Find "No throttling" dropdown
4. Select a preset or create custom

**Presets available:**

| Profile | Speed | Latency | Use Case |
|---------|-------|---------|----------|
| Fast 3G | 1.5 Mbps | 40ms | Average mobile |
| Slow 3G | 750 Kbps | 100ms | Poor connection |
| Offline | 0 | ∞ | Test offline support |

### CPU Throttling

**How to enable:**

1. Open DevTools → Performance tab
2. Click ⚙️ Settings
3. Select 4x or 6x slowdown

**Why throttle CPU?**

- Your dev machine has fast processor
- Average smartphone is much slower
- Animations that work fine for you may be janky for users

---

## 1.7 Performance Budgets

### What is a Performance Budget?

**Definition:** Pre-defined limits for metrics that you don't want to exceed.

**Analogy:** Like a financial budget but for performance. "We will not let our page exceed 500KB or take more than 3 seconds to load."

### Example Performance Budget

| Metric | Budget |
|--------|--------|
| Page Weight | < 500 KB |
| LCP | < 2.5 seconds |
| TBT | < 200 ms |
| JavaScript | < 200 KB |
| Images | < 300 KB |
| Requests | < 50 |

### Enforcing Budgets

Performance budgets can be integrated into your build process to warn or fail when exceeded. This prevents performance regressions over time.

---

## 1.8 Unit I Summary

### Key Concepts Learned

**Web Performance** = Speed + Efficiency + Responsiveness

**Core Web Vitals (Google's top 3 metrics):**

| Metric | Measures | Good Score |
|--------|----------|------------|
| LCP | Loading | ≤ 2.5s |
| INP | Interactivity | ≤ 200ms |
| CLS | Visual Stability | ≤ 0.1 |

**Other Important Metrics:**

- **TTFB** - Server response time
- **FCP** - First content visible
- **TBT** - Time browser was blocked
- **TTI** - Page fully interactive
- **Speed Index** - Visual progress speed

**Assessment Tools:**

- PageSpeed Insights - Free Google tool
- Chrome DevTools - Built-in browser tools
- Lighthouse - Automated audits
- WebPageTest - Detailed waterfall analysis

---

# Unit II: CSS Optimization & Critical CSS

## 2.1 Understanding CSS Performance

### How CSS Affects Page Loading

**Key fact:** CSS is "render-blocking" by default.

> **What does render-blocking mean?**
> The browser will NOT show anything on screen until ALL your CSS is downloaded and processed. Even if your HTML is ready, users see a blank page while waiting for CSS.

**Why is CSS render-blocking?**
The browser needs to know styles before painting. Otherwise:

- Text might appear then change font
- Layouts would jump around
- Colors would switch suddenly

### The Problem with Large CSS Files

```
Scenario: 500KB CSS file on slow 3G connection

Download time: 500KB ÷ 750Kbps ≈ 5.3 seconds
Result: User sees NOTHING for 5+ seconds!
```

This is why CSS optimization is crucial.

---

## 2.2 Mobile-First CSS

### What is Mobile-First Design?

**Definition:** Writing your base CSS for mobile screens, then adding styles for larger screens using media queries.

**The old way (Desktop-First):**

```css
/* Start with desktop styles */
.container { width: 1200px; }

/* Override for mobile */
@media (max-width: 768px) {
  .container { width: 100%; }
}
```

**The better way (Mobile-First):**

```css
/* Start with mobile styles */
.container { width: 100%; }

/* Enhance for desktop */
@media (min-width: 768px) {
  .container { width: 1200px; }
}
```

### Why Mobile-First is Better for Performance

1. **Mobile devices download less CSS initially**
   - Base styles are simple and small
   - Complex desktop styles only download if needed

2. **Progressive Enhancement**
   - Start with essentials
   - Add features for capable devices

3. **Matches Google's approach**
   - Google uses "mobile-first indexing"
   - Your mobile site is what Google evaluates

---

## 2.3 CSS Performance Best Practices

### Keep Selectors Simple

**The browser reads selectors RIGHT to LEFT:**

```css
/* Browser reads: find all "a" → filter to "li" → filter to "ul" → filter to ".nav" */
.nav ul li a { }

/* Much faster - direct class lookup */
.nav-link { }
```

### Avoid Expensive Properties

Some CSS properties are more expensive (slow) to render:

**Expensive (use carefully):**

- `box-shadow`
- `filter`
- `opacity` (when animating)
- `position: fixed`

**Fast:**

- `transform`
- `color`
- `background-color`

### Remove Unused CSS

**Shocking fact:** The average website has 35-50% unused CSS.

**How to find unused CSS:**

1. Chrome DevTools → Coverage panel
2. Press record (🔴)
3. Load your page
4. Red bars = unused CSS

---

## 2.4 Critical CSS

### What is Critical CSS?

**Definition:** The minimum CSS required to render the "above-the-fold" content (what users see before scrolling).

**Above the fold** = The portion of the webpage visible without scrolling.

### Why Critical CSS Matters

**Without Critical CSS:**

```
1. Browser downloads HTML
2. Browser discovers CSS link
3. Browser downloads entire CSS file (could be 500KB)
4. Browser processes CSS
5. FINALLY shows content to user
```

**With Critical CSS:**

```
1. Browser downloads HTML (contains inline critical CSS)
2. Browser immediately shows above-the-fold content!
3. Rest of CSS loads in background
4. Complete styling applied when ready
```

### How to Implement Critical CSS

**Step 1: Identify above-the-fold content**

- Usually: header, navigation, hero section
- First ~600-800 pixels of content

**Step 2: Extract styles for that content**

- Only styles needed for visible elements
- Usually 10-20KB instead of 100KB+

**Step 3: Inline critical CSS in HTML**

```html
<head>
  <style>
    /* Critical CSS here - loads immediately */
    .header { background: blue; }
    .hero { padding: 50px; }
  </style>
  
  <!-- Rest of CSS loads asynchronously -->
  <link rel="preload" href="styles.css" as="style" 
        onload="this.rel='stylesheet'">
</head>
```

---

## 2.5 CSS Transitions and Animations

### Performance-Friendly Animations

**Two properties are "free" to animate:**

1. `transform` (rotate, scale, translate)
2. `opacity` (fade in/out)

**Why are they free?**
These properties use the **GPU** (graphics card) instead of CPU. The browser creates a separate "layer" that can animate without affecting other content.

### What NOT to Animate

**Expensive properties that cause "reflow":**

- `width` / `height`
- `top` / `left` / `right` / `bottom`
- `margin` / `padding`
- `font-size`

**Example: Slide-in animation**

```css
/* ❌ SLOW - animates 'left' (causes reflow) */
.slide-in {
  position: absolute;
  left: -100%;
  transition: left 0.3s;
}
.slide-in.active {
  left: 0;
}

/* ✅ FAST - animates 'transform' (GPU accelerated) */
.slide-in {
  transform: translateX(-100%);
  transition: transform 0.3s;
}
.slide-in.active {
  transform: translateX(0);
}
```

---

## 2.6 Unit II Summary

**CSS is render-blocking:**

- Browser waits for ALL CSS before painting
- This is why CSS optimization matters

**Mobile-First approach:**

- Write base styles for mobile
- Add desktop styles with media queries
- Results in smaller initial CSS

**Critical CSS:**

- Inline the CSS needed for above-the-fold
- Load remaining CSS asynchronously
- Dramatically improves FCP and LCP

**Animation performance:**

- Animate only `transform` and `opacity`
- Avoid animating width, height, position properties
- Use `will-change` hint for complex animations

---

# Unit III: Image Optimization

## 3.1 Why Image Optimization Matters

### The Image Problem

**Images typically account for 50-70% of a webpage's total size.**

| Website Component | Typical Size |
|-------------------|--------------|
| Images | 50-70% |
| JavaScript | 20-25% |
| CSS | 5-10% |
| HTML | 2-5% |
| Fonts | 5-10% |

**Impact of unoptimized images:**

- Slow page loads
- High bandwidth costs
- Poor Core Web Vitals
- Frustrated users on mobile

---

## 3.2 Image Formats Explained

### Understanding Different Image Types

#### JPEG (Joint Photographic Experts Group)

**Best for:** Photographs, images with many colors

**Characteristics:**

- 16 million colors
- Lossy compression (quality reduces with compression)
- No transparency support
- Small file sizes for photos

#### PNG (Portable Network Graphics)

**Best for:** Graphics, logos, images needing transparency

**Two types:**

- **PNG-8:** 256 colors, small files
- **PNG-24:** 16 million colors, larger files

**Characteristics:**

- Lossless compression
- Supports transparency
- Larger than JPEG for photos

#### GIF (Graphics Interchange Format)

**Best for:** Simple animations

**Characteristics:**

- Only 256 colors
- Supports animation
- Supports transparency (but only on/off, no partial transparency)
- Outdated - use WebP instead

#### SVG (Scalable Vector Graphics)

**Best for:** Icons, logos, illustrations

**Characteristics:**

- Vector format (scales infinitely without blur)
- Usually tiny file size
- Can be styled with CSS
- Can be animated

#### WebP (Web Picture Format)

**Best for:** Everything! (Modern replacement for JPEG/PNG)

**Characteristics:**

- 25-35% smaller than JPEG at same quality
- Supports transparency
- Supports animation
- 96%+ browser support

#### AVIF (AV1 Image Format)

**Best for:** Maximum compression (newest format)

**Characteristics:**

- 50% smaller than JPEG
- Excellent quality
- Growing browser support (~90%)
- Slower to encode

### Which Format to Use?

| Situation | Recommended Format |
|-----------|-------------------|
| Photo | WebP > AVIF > JPEG |
| Logo/Icon | SVG > WebP > PNG |
| Graphic with transparency | WebP > PNG |
| Simple animation | WebP > GIF |
| Need maximum compatibility | JPEG/PNG with WebP fallback |

---

## 3.3 Responsive Images

### The Problem with Single-Size Images

**Old approach:**

```html
<img src="hero.jpg">  <!-- Same 2000px image for all devices -->
```

**Problems:**

- Phone users download huge image they can't display fully
- Desktop users might get too small an image
- Wastes bandwidth on mobile

### Solution: srcset and sizes

**srcset** tells the browser what images are available:

```html
<img src="hero-800.jpg"
     srcset="hero-400.jpg 400w,
             hero-800.jpg 800w,
             hero-1200.jpg 1200w,
             hero-1600.jpg 1600w"
     sizes="(max-width: 600px) 100vw,
            (max-width: 1200px) 50vw,
            800px"
     alt="Hero image">
```

**Explanation:**

- `srcset`: List of images with their widths (400w means 400 pixels wide)
- `sizes`: Tells browser how big the image will display
- Browser automatically chooses the best image

### The picture Element

**For format fallbacks and art direction:**

```html
<picture>
  <!-- Try AVIF first (smallest) -->
  <source type="image/avif" srcset="hero.avif">
  
  <!-- Fall back to WebP -->
  <source type="image/webp" srcset="hero.webp">
  
  <!-- Ultimate fallback to JPEG -->
  <img src="hero.jpg" alt="Hero image" width="800" height="600">
</picture>
```

---

## 3.4 Lazy Loading

### What is Lazy Loading?

**Definition:** Only loading images when they're about to become visible.

**Without lazy loading:**

```
Page loads → ALL 50 images download immediately
(Even images at bottom of page that user might never scroll to)
```

**With lazy loading:**

```
Page loads → Only visible images download
User scrolls → Next images download just before becoming visible
```

### Implementing Lazy Loading

**Native lazy loading (simplest):**

```html
<img src="photo.jpg" loading="lazy" alt="Photo" width="800" height="600">
```

**Important:** Don't lazy load above-the-fold images!

```html
<!-- Hero image - load immediately -->
<img src="hero.jpg" loading="eager" alt="Hero" width="1200" height="600">

<!-- Below-fold images - lazy load -->
<img src="product1.jpg" loading="lazy" alt="Product" width="400" height="300">
```

### Why Include width and height?

**Without dimensions:**

```
Image space is 0 initially
   ↓
Image loads
   ↓
Page layout JUMPS to make room (CLS!)
```

**With dimensions:**

```
Browser reserves correct space from start
   ↓
Image loads
   ↓
Image appears smoothly in reserved space (no CLS!)
```

---

## 3.5 Image Sprites

### What is an Image Sprite?

**Definition:** Combining multiple small images into one large image to reduce HTTP requests.

**Without sprites:**

```
10 icon files = 10 HTTP requests
```

**With sprites:**

```
1 sprite file = 1 HTTP request
```

### How Sprites Work

```css
.icon {
    background-image: url('sprites.png');
    background-repeat: no-repeat;
    width: 32px;
    height: 32px;
}

/* Position the sprite to show each icon */
.icon-home   { background-position: 0 0; }
.icon-search { background-position: -32px 0; }
.icon-cart   { background-position: -64px 0; }
```

### When to Use Sprites in 2024

**Less important now because:**

- HTTP/2 allows many parallel requests
- SVG icons are often better
- Icon fonts are another option

**Still useful for:**

- HTTP/1.1 servers
- Sites with many small PNG icons
- Retro/game-style graphics

---

## 3.6 Unit III Summary

**Image optimization is crucial:**

- Images are 50-70% of page weight
- Unoptimized images destroy performance

**Format selection:**

| Need | Best Format |
|------|-------------|
| Photos | WebP > AVIF > JPEG |
| Icons | SVG |
| Graphics | WebP > PNG |

**Responsive images:**

- Use `srcset` for different sizes
- Use `<picture>` for format fallbacks
- Let browser choose optimal image

**Lazy loading:**

- Use `loading="lazy"` for below-fold images
- Never lazy load hero images
- Always include width/height to prevent CLS

---

# Unit IV: Fonts & JavaScript Optimization

## 4.1 Web Fonts and Performance

### The Font Loading Problem

**What happens when using custom fonts:**

```
1. HTML loads
2. CSS loads → references custom font
3. Browser downloads font file
4. MEANWHILE: Text is invisible (FOIT) or shows fallback (FOUT)
5. Font loads → Text appears in custom font
```

**FOIT (Flash of Invisible Text)**

- Text is hidden until font loads
- Bad for users who want to read content

**FOUT (Flash of Unstyled Text)**

- Text shows in fallback font, then swaps
- Slightly jarring but readable

### Font Loading Strategies

**font-display property:**

```css
@font-face {
    font-family: 'CustomFont';
    src: url('font.woff2') format('woff2');
    font-display: swap; /* Recommended */
}
```

| Value | Behavior | Best For |
|-------|----------|----------|
| `auto` | Browser decides | Not recommended |
| `block` | Hide text up to 3s | Brand fonts |
| `swap` | Show fallback immediately | Most cases ✅ |
| `fallback` | Hide briefly, then swap | Balance |
| `optional` | Very brief hide, may skip | Performance-first |

---

## 4.2 Font Formats

### Understanding Font File Types

| Format | Size | Browser Support | Recommendation |
|--------|------|-----------------|----------------|
| **WOFF2** | Smallest | 97%+ | ✅ Use First |
| WOFF | Small | 99%+ | Fallback |
| TTF | Large | 99%+ | Legacy |
| EOT | Large | IE only | Don't use |

### Modern Font Stack

```css
@font-face {
    font-family: 'MyFont';
    src: url('font.woff2') format('woff2'),
         url('font.woff') format('woff');
    font-display: swap;
}

body {
    font-family: 'MyFont', 
                 system-ui, 
                 -apple-system, 
                 sans-serif;
}
```

---

## 4.3 Font Subsetting

### What is Subsetting?

**Definition:** Removing unused characters from a font file.

**Example:**

- Full font with all languages: 250KB
- Subset with only Latin characters: 25KB
- 90% smaller!

### How to Subset Fonts

**For Latin-only websites:**

```html
<!-- Google Fonts with subset -->
<link href="https://fonts.googleapis.com/css2?family=Roboto&subset=latin" rel="stylesheet">
```

**unicode-range (browser loads only what's needed):**

```css
@font-face {
    font-family: 'MyFont';
    src: url('font-latin.woff2') format('woff2');
    unicode-range: U+0000-00FF; /* Latin characters only */
}
```

---

## 4.4 JavaScript Loading

### How JavaScript Blocks the Page

**The problem:**

```html
<head>
    <script src="app.js"></script>  <!-- BLOCKS everything! -->
</head>
```

When the browser encounters a `<script>` tag:

1. Stop parsing HTML
2. Download the script
3. Execute the script
4. Then continue parsing HTML

**This blocks the page from loading/displaying!**

### Script Loading Attributes

#### async

```html
<script src="analytics.js" async></script>
```

- Downloads in parallel with HTML parsing
- Executes immediately when downloaded (may interrupt parsing)
- Use for: Independent scripts (analytics, ads)

#### defer

```html
<script src="app.js" defer></script>
```

- Downloads in parallel with HTML parsing
- Executes AFTER HTML is fully parsed
- Maintains script order
- Use for: Main application scripts

#### type="module"

```html
<script type="module" src="app.js"></script>
```

- Modern ES6 modules
- Deferred by default
- Strict mode

### Visual Comparison

```
Without defer/async:
HTML: ████████─────────████████████████████████
             ↑ stop ↑ run JS

With async:
HTML: ████████████████████████████████████████
      └───JS───┘↑ run (might interrupt)

With defer:
HTML: ████████████████████████████████████████→done
      └───JS────────────────────────────┘↑ run
```

---

## 4.5 Reducing JavaScript

### The Cost of JavaScript

JavaScript is expensive because:

1. **Download** - Takes time to transfer
2. **Parse** - Browser must read the code
3. **Compile** - Browser converts to machine code
4. **Execute** - Browser runs the code

**Same 100KB:**

- Image: Only download cost
- JavaScript: Download + Parse + Compile + Execute

### Do You Need That Library?

**jQuery example:**

- jQuery: 87KB
- The 5 jQuery features you actually use: ~10KB of vanilla JS

**Common jQuery replacements:**

```javascript
// jQuery: $(document).ready()
// Vanilla: 
document.addEventListener('DOMContentLoaded', () => { });

// jQuery: $('.item')
// Vanilla:
document.querySelectorAll('.item')

// jQuery: $.ajax()
// Vanilla:
fetch(url).then(r => r.json())
```

---

## 4.6 requestAnimationFrame

### What is requestAnimationFrame?

**Definition:** A method that tells the browser you want to perform an animation, letting the browser optimize the animation for smooth performance.

### Why Not setTimeout/setInterval?

```javascript
// ❌ Bad: Arbitrary timing
setInterval(() => {
    updateAnimation();
}, 16); // Trying to hit 60fps (1000/60 ≈ 16ms)
```

**Problems:**

- May run when tab is not visible (wasting battery)
- May not sync with screen refresh
- Can cause "jank" (stuttering)

```javascript
// ✅ Good: Browser-optimized
function animate() {
    updateAnimation();
    requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```

**Benefits:**

- Syncs with screen refresh rate (60fps)
- Pauses when tab is hidden
- Optimized by browser

---

## 4.7 Unit IV Summary

**Font optimization:**

- Use WOFF2 format
- Use `font-display: swap`
- Subset fonts to reduce size
- Preload critical fonts

**JavaScript optimization:**

- Use `defer` for main scripts
- Use `async` for independent scripts
- Consider vanilla JS over jQuery
- Tree-shake unused code

**Animation:**

- Use requestAnimationFrame, not setTimeout
- Animate only transform and opacity
- Browser optimizes for 60fps

---

# Unit V: Service Workers & Asset Delivery

## 5.1 What is a Service Worker?

### Simple Explanation

**A Service Worker is like a helpful assistant that lives in your browser** and can:

- Save files for offline use
- Intercept network requests
- Work in the background even when the page is closed

**Analogy:** Imagine having a personal assistant who:

- Keeps copies of important documents (caching)
- Can answer simple questions without calling the office (offline support)
- Keeps working even when you're not watching (background sync)

### Service Worker Lifecycle

```
Registration → Installation → Activation → Idle/Working
                    ↓               ↓
               Cache files    Clean old caches
```

### What Service Workers Enable

1. **Offline Support** - Website works without internet
2. **Faster Loading** - Serve from cache instead of network
3. **Push Notifications** - Send alerts even when site is closed
4. **Background Sync** - Sync data when connection is restored

---

## 5.2 Caching Strategies Explained

### Cache First

**"Check the filing cabinet before making a phone call"**

1. Look in cache
2. If found → Return cached version
3. If not found → Fetch from network

**Best for:** Static assets (CSS, JS, images)

### Network First

**"Always try to get the latest, but have a backup"**

1. Try to fetch from network
2. If successful → Return response (and cache it)
3. If network fails → Return cached version

**Best for:** Dynamic content (API data, news articles)

### Stale While Revalidate

**"Give them what you have now, but check for updates"**

1. Return cached version immediately
2. Fetch fresh version in background
3. Update cache for next time

**Best for:** Balance between speed and freshness (social feeds, blogs)

---

## 5.3 Asset Compression

### What is Compression?

**Definition:** Making files smaller by encoding them efficiently.

**Analogy:** Instead of writing "AAAABBBCCCC", write "4A3B4C". Same information, fewer characters.

### Compression Types

| Algorithm | Size Reduction | Speed | Use Case |
|-----------|---------------|-------|----------|
| **Gzip** | 70-80% | Fast | Standard choice |
| **Brotli** | 80-90% | Slower | Better compression |

**How compression works:**

```
Original CSS: 100KB
Gzipped: 25KB (75% smaller)
Brotli: 20KB (80% smaller)
```

### Enabling Compression

Compression is enabled on the **server side**. The browser automatically decompresses.

**How it works:**

1. Browser sends: "I accept gzip, br" (Accept-Encoding header)
2. Server sends compressed file
3. Browser decompresses automatically
4. You see normal content

---

## 5.4 HTTP Caching

### What is HTTP Caching?

**Definition:** Telling the browser to save files locally so they don't need to be downloaded again.

### Cache-Control Header

The server sends instructions about how long to cache:

```
Cache-Control: max-age=31536000
```

**Translation:** "Save this file for 31,536,000 seconds (1 year)"

### Common Cache-Control Values

| Value | Meaning |
|-------|---------|
| `max-age=3600` | Cache for 1 hour |
| `max-age=31536000` | Cache for 1 year |
| `no-cache` | Always check if file changed |
| `no-store` | Never save this file |
| `immutable` | This file will never change |

### Cache-Busting

**Problem:** If you cache a file for 1 year but need to update it tomorrow, users have the old version.

**Solution:** Change the filename when content changes.

```html
<!-- Before update -->
<link href="styles.v1.css">

<!-- After update -->
<link href="styles.v2.css">

<!-- Or use hashes -->
<link href="styles.a3f5c2.css">
```

Browser sees new filename → Downloads new file

---

## 5.5 CDN (Content Delivery Network)

### What is a CDN?

**Definition:** A network of servers around the world that store copies of your files.

**Without CDN:**

```
User in Tokyo → Requests file → Server in New York
Latency: 200ms round trip
```

**With CDN:**

```
User in Tokyo → Requests file → CDN server in Tokyo
Latency: 20ms round trip
```

### How CDN Works

1. You upload files to CDN
2. CDN copies files to servers worldwide
3. User requests file
4. CDN serves from nearest server

### Popular CDNs

| CDN | Known For |
|-----|-----------|
| Cloudflare | Free tier, security features |
| AWS CloudFront | Amazon integration |
| Fastly | Speed, edge computing |
| Akamai | Enterprise, global reach |

---

## 5.6 Resource Hints

### Helping the Browser Plan Ahead

**Resource hints** tell the browser about resources it will need soon.

### Types of Resource Hints

#### dns-prefetch

**"Start looking up this domain's IP address now"**

```html
<link rel="dns-prefetch" href="//fonts.googleapis.com">
```

**When to use:** Third-party domains you'll need

---

#### preconnect

**"Set up a full connection to this server now"**

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
```

**What it does:**

- DNS lookup
- TCP connection
- TLS handshake

**When to use:** Critical third-party resources

---

#### prefetch

**"Download this file when you have time - I'll need it later"**

```html
<link rel="prefetch" href="/next-page.html">
```

**When to use:** Resources for the next likely page

---

#### preload

**"Download this file RIGHT NOW - I need it for this page"**

```html
<link rel="preload" href="/critical.css" as="style">
<link rel="preload" href="/hero.webp" as="image">
<link rel="preload" href="/font.woff2" as="font" crossorigin>
```

**When to use:** Critical resources for current page

---

## 5.7 Unit V Summary

**Service Workers:**

- JavaScript that runs in background
- Enables offline support and caching
- Creates faster repeat visits

**Caching Strategies:**

| Strategy | Use For |
|----------|---------|
| Cache First | Static assets |
| Network First | Dynamic content |
| Stale While Revalidate | Balance |

**Compression:**

- Gzip: 70-80% smaller
- Brotli: 80-90% smaller (better)

**CDN:**

- Serves files from nearest server
- Reduces latency dramatically

**Resource Hints:**

| Hint | Purpose |
|------|---------|
| preload | Critical current page resources |
| prefetch | Future page resources |
| preconnect | Establish server connection |
| dns-prefetch | Resolve domain early |

---

# Unit VI: HTTP/2 & Gulp Automation

## 6.1 Understanding HTTP

### What is HTTP?

**HTTP (HyperText Transfer Protocol)** is the language browsers and servers use to communicate.

**Simple analogy:** HTTP is like the rules of conversation. Both sides need to agree on how to talk to each other.

### HTTP/1.1 Problems

HTTP/1.1 was created in 1997 and has limitations:

1. **Head-of-line blocking**
   - Browser can only send one request at a time per connection
   - Like a single-lane road - one car must wait for another

2. **Limited parallel connections**
   - Browsers open only 6-8 connections per domain
   - Limits how many files can download simultaneously

3. **Uncompressed headers**
   - Every request sends all headers (cookies, etc.)
   - Wastes bandwidth sending same info repeatedly

4. **No prioritization**
   - Can't say "download this file first, it's urgent!"

---

## 6.2 HTTP/2 Benefits

HTTP/2 (2015) solves these problems:

### Multiplexing

**"Multiple files over one connection"**

```
HTTP/1.1:
Connection 1: ──file1──────wait──────file2───
Connection 2: ────file3────wait────file4─────
Connection 3: ──────file5────wait────file6───

HTTP/2:
Connection 1: ──file1──file2──file3──file4──file5──file6──
(All interleaved over single connection!)
```

### Header Compression (HPACK)

- Headers are compressed and cached
- Repeat requests don't resend same headers
- Saves bandwidth

### Server Push

- Server can send files before browser asks
- "You'll need this CSS, here it is!"

### Stream Prioritization

- Browser can say "I need the CSS before images"
- Critical resources load first

---

## 6.3 HTTP/2 Changes Optimization Strategies

**Old HTTP/1.1 tricks that are NOW UNNECESSARY:**

| Old Trick | Why It Was Done | HTTP/2 Reality |
|-----------|----------------|----------------|
| Domain Sharding | Open more connections | One connection is efficient |
| Image Sprites | Fewer HTTP requests | Many requests are fine |
| CSS/JS Concatenation | Fewer HTTP requests | Separate files are fine |
| Inlining small resources | Avoid requests | Requests are cheap now |

**What still matters with HTTP/2:**

- Compression (gzip/brotli)
- Proper caching
- Image optimization
- Critical CSS

---

## 6.4 Server Push

### What is Server Push?

**Definition:** The server sends resources to the browser before the browser asks for them.

**Normal flow:**

```
Browser: "Give me HTML"
Server: "Here's HTML"
Browser: "Oh, I need styles.css"
Server: "Here's CSS"
Browser: "Oh, I need app.js"
Server: "Here's JS"
```

**With Server Push:**

```
Browser: "Give me HTML"
Server: "Here's HTML... and CSS... and JS you'll need"
(All at once!)
```

### When to Use Server Push

**Good candidates for push:**

- Critical CSS
- Main JavaScript bundle
- Web fonts used above-the-fold
- Hero image

**Don't push:**

- Resources already in browser cache
- Large files
- Resources not needed immediately

---

## 6.5 Introduction to Gulp

### What is Gulp?

**Gulp is a task runner** - a tool that automates repetitive tasks.

**Without Gulp:**

1. Manually compress images
2. Manually minify CSS
3. Manually minify JavaScript
4. Manually copy files
5. Repeat every time you make changes...

**With Gulp:**

```bash
gulp build  # Does ALL of the above automatically!
```

### What Can Gulp Automate?

- **Minification** - Making files smaller
- **Compilation** - Sass → CSS, TypeScript → JavaScript
- **Optimization** - Compress images
- **Watching** - Auto-run tasks when files change
- **Live Reload** - Refresh browser automatically
- **Testing** - Run tests automatically

---

## 6.6 Gulp Concepts

### Tasks

**A task is a function that does something specific.**

```javascript
function minifyCSS() {
    // Code to minify CSS files
}
```

### Pipes

**Pipes connect steps together.**

Think of it like an assembly line:

```
Source files → Transform 1 → Transform 2 → Output
```

### Watch

**Watch monitors files and runs tasks when they change.**

```javascript
watch('src/*.css', minifyCSS);
// Whenever any CSS file changes, run minifyCSS
```

---

## 6.7 Essential Gulp Plugins

| Plugin | Purpose |
|--------|---------|
| gulp-clean-css | Minify CSS |
| gulp-uglify | Minify JavaScript |
| gulp-htmlmin | Minify HTML |
| gulp-imagemin | Optimize images |
| gulp-sass | Compile Sass to CSS |
| gulp-concat | Combine files |
| gulp-rename | Rename files |
| browser-sync | Live reload |

---

## 6.8 Unit VI Summary

**HTTP/2 improvements:**

- Multiplexing (many files, one connection)
- Header compression
- Server push
- Stream prioritization

**Optimization changes with HTTP/2:**

- Domain sharding → Not needed
- Sprites/concatenation → Less important
- Compression/caching → Still essential

**Gulp automation:**

- Automates repetitive tasks
- Save time and reduce errors
- Essential for build pipelines

---

# Practicals

## Practical 1: Minifying Assets

**Objective:** Reduce file sizes by removing unnecessary characters.

**What is minification?**
Removing whitespace, comments, and shortening variable names.

**Before minification:**

```css
/* Main container styles */
.container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}
```

**After minification:**

```css
.container{width:100%;max-width:1200px;margin:0 auto;padding:20px}
```

**Savings:** Often 20-40% smaller files!

---

## Practical 2: Installing Node.js and Git

**Node.js** - JavaScript runtime that lets you run JavaScript outside browsers. Required for most build tools.

**Git** - Version control system for tracking code changes.

**Installation:**

```bash
# Check if Node is installed
node --version

# Check if Git is installed
git --version
```

---

## Practical 3: Benchmarking JavaScript

**Why benchmark?**
To find slow code that might cause TBT issues.

**Simple timing:**

```javascript
console.time('operation');
// Code to measure
console.timeEnd('operation');
// Output: operation: 45.234ms
```

---

## Practical 4: Working with SVG Images

**SVG advantages:**

- Infinitely scalable (vector)
- Usually smallest file size for icons
- Can be styled with CSS
- Can be animated

**Using inline SVG:**

```html
<svg width="24" height="24" viewBox="0 0 24 24">
    <path d="M12 2L2 7v10l10 5 10-5V7z"/>
</svg>
```

---

## Practical 5: Media Queries

**Purpose:** Apply different styles based on screen size.

**Mobile-first approach:**

```css
/* Base: Mobile */
.container { width: 100%; }

/* Tablet and up */
@media (min-width: 768px) {
    .container { width: 750px; }
}

/* Desktop */
@media (min-width: 1024px) {
    .container { width: 970px; }
}
```

---

## Practical 6: Font Subsetting

**Goal:** Reduce font file size by including only needed characters.

**Commands:**

```bash
# Install fonttools
pip install fonttools

# Create Latin-only subset
pyftsubset font.ttf --unicodes="U+0000-00FF" --output-file=font-latin.woff2
```

**Result:** 250KB → 25KB (90% smaller!)

---

## Practical 7: requestAnimationFrame Animation

**Goal:** Create smooth, efficient animations.

```javascript
function animate() {
    // Update animation
    element.style.transform = `translateX(${position}px)`;
    
    // Continue animation
    requestAnimationFrame(animate);
}

// Start
requestAnimationFrame(animate);
```

---

## Practical 8: Creating a Service Worker

**Basic service worker for caching:**

```javascript
// In main.js - Register service worker
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
}

// sw.js - Service worker file
const CACHE_NAME = 'my-site-v1';
const urlsToCache = ['/', '/styles.css', '/app.js'];

self.addEventListener('install', event => {
    event.waitUntil(
        caches.open(CACHE_NAME)
            .then(cache => cache.addAll(urlsToCache))
    );
});

self.addEventListener('fetch', event => {
    event.respondWith(
        caches.match(event.request)
            .then(response => response || fetch(event.request))
    );
});
```

---

## Practical 9: Caching Assets with Cache-Control

**Server configuration example (Nginx):**

```nginx
# Cache static assets for 1 year
location ~* \.(css|js|png|jpg|webp)$ {
    add_header Cache-Control "max-age=31536000, immutable";
}

# Don't cache HTML
location ~* \.html$ {
    add_header Cache-Control "no-cache";
}
```

---

## Practical 10: HTTP/2 Server Push

**Nginx configuration:**

```nginx
location / {
    http2_push /styles.css;
    http2_push /app.js;
}
```

---

## Practical 11: Creating Gulp Tasks

**Complete gulpfile.js:**

```javascript
const gulp = require('gulp');
const cleanCSS = require('gulp-clean-css');
const uglify = require('gulp-uglify');

// Minify CSS
function styles() {
    return gulp.src('src/css/*.css')
        .pipe(cleanCSS())
        .pipe(gulp.dest('dist/css'));
}

// Minify JavaScript
function scripts() {
    return gulp.src('src/js/*.js')
        .pipe(uglify())
        .pipe(gulp.dest('dist/js'));
}

// Watch for changes
function watch() {
    gulp.watch('src/css/*.css', styles);
    gulp.watch('src/js/*.js', scripts);
}

// Export tasks
exports.styles = styles;
exports.scripts = scripts;
exports.watch = watch;
exports.default = gulp.series(styles, scripts);
```

---

# Course Summary

## What You've Learned

| Unit | Key Topics |
|------|------------|
| **I** | Performance metrics (LCP, INP, CLS, TBT, TTFB), assessment tools |
| **II** | CSS optimization, mobile-first, critical CSS |
| **III** | Image formats, responsive images, lazy loading |
| **IV** | Font loading, JavaScript optimization, requestAnimationFrame |
| **V** | Service workers, caching, CDN, resource hints |
| **VI** | HTTP/2, server push, Gulp automation |

## Key Performance Metrics Quick Reference

| Metric | Full Name | What It Measures | Good Score |
|--------|-----------|------------------|------------|
| **LCP** | Largest Contentful Paint | Main content loading | ≤ 2.5s |
| **INP** | Interaction to Next Paint | Page responsiveness | ≤ 200ms |
| **CLS** | Cumulative Layout Shift | Visual stability | ≤ 0.1 |
| **TTFB** | Time to First Byte | Server response | ≤ 800ms |
| **FCP** | First Contentful Paint | First content visible | ≤ 1.8s |
| **TBT** | Total Blocking Time | Main thread blocking | ≤ 200ms |
| **TTI** | Time to Interactive | Full interactivity | ≤ 3.8s |

## Optimization Checklist

**Loading:**

- [ ] Enable compression (gzip/brotli)
- [ ] Use CDN
- [ ] Implement browser caching
- [ ] Minify CSS, JavaScript, HTML

**Images:**

- [ ] Use modern formats (WebP, AVIF)
- [ ] Implement lazy loading
- [ ] Specify width/height attributes
- [ ] Use responsive images

**CSS:**

- [ ] Implement Critical CSS
- [ ] Remove unused CSS
- [ ] Use mobile-first approach

**JavaScript:**

- [ ] Use defer/async attributes
- [ ] Remove unused code
- [ ] Use requestAnimationFrame for animations

**Fonts:**

- [ ] Use WOFF2 format
- [ ] Subset fonts
- [ ] Use font-display: swap
- [ ] Preload critical fonts

---

## References

1. **Website Optimization: An Hour a Day** by Rich Page, Sybex
2. **High Performance Web Sites** by Steve Souders, O'Reilly
3. **Web Performance Daybook** by Stoyan Stefanov, O'Reilly
4. **Web Performance in Action** by Jeremy Wagner, Manning Publications

---

*End of CAP785 Web Performance Optimization Guide*
