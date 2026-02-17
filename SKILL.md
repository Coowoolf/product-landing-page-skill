---
name: Product Landing Page Generator
description: Generate a premium single-page product website from a single product image, with inline SVG illustrations, app mockups, engineering drawings, and stunning design aesthetics.
---

# Product Landing Page Generator

Turn a single product image into a complete, premium product landing page — with AI-generated SVG illustrations, orthographic engineering drawings, app mockups, and a cohesive design system. All output is a **single self-contained HTML file**.

## Input Requirements

| Input | Required | Description |
|-------|----------|-------------|
| Product image | ✅ | A photo, render, or sketch of the product |
| Product name | ❌ | If not provided, invent a fitting brand name |
| Product category | ❌ | e.g. "audio amplifier", "smart speaker" — will be inferred from image if not given |
| Design philosophy | ❌ | e.g. "Dieter Rams", "Apple minimalism", "Brutalist" — defaults to minimalist |
| Style preset | ❌ | See presets below |

### Style Presets

| Preset | Accent Color | Font | Vibe |
|--------|-------------|------|------|
| `rams` | `#E85D2A` (Braun orange) | Inter/Helvetica Neue | Clean, functional, honest |
| `apple` | `#0071E3` (Apple blue) | SF Pro/Inter | Premium, spacious, invisible design |
| `muji` | `#B22222` (MUJI red) | Noto Sans | Warm, natural, unadorned |
| `bang-olufsen` | `#C5A258` (Gold) | Playfair Display | Luxurious, sculptural |
| `teenage-engineering` | `#FF6600` (TE orange) | Space Mono | Playful, technical, retro-futuristic |
| `custom` | User-specified | User-specified | User-specified |

## Workflow

### Phase 1: Image Analysis

Study the uploaded product image carefully and extract:

1. **Form Factor** — rectangular box? cylindrical? irregular? What are the approximate proportions (W:H:D)?
2. **Key Visual Features** — buttons, knobs, ports, displays, ventilation, logos, LEDs
3. **Materials & Finishes** — brushed aluminum, matte plastic, wood, glass, mesh fabric
4. **Color Palette** — dominant colors from the product itself
5. **Design Era/School** — does it evoke Braun/Rams? Apple? Bauhaus? Industrial?
6. **Functional Hints** — what does this product likely do? What inputs/outputs?

Document these observations mentally before proceeding.

### Phase 2: Product Narrative Construction

Based on the image analysis, construct a complete fictional product identity:

```
Brand Name:       [e.g. "SoulRich", "Aether", "MOTO"]
Model Number:     [e.g. "T-100", "Pro Max", "Series 7"]
Tagline:          [e.g. "Sound. Perfected.", "Less but better."]
Category:         [e.g. High-end tube amplifier]
Price Point:      [implied by design — luxury/mid/entry]
Design Philosophy: [1-2 sentences]
Key Specs:        [4-6 headline numbers, e.g. "100W", "24-bit/192kHz"]
Features:         [4 features, each with name + description + 1-2 spec values]
Full Spec Sheet:  [2-3 categories × 4-6 rows each]
```

### Phase 3: Page Architecture

The page follows a **scrolling narrative structure** (Apple product page style). Each section occupies roughly one viewport height.

```
┌─────────────────────────────────────────┐
│  NAVBAR (fixed, semi-transparent)       │
│  Brand • Section links                  │
├─────────────────────────────────────────┤
│  HERO                                   │
│  Giant product name + tagline           │
│  Product image (the uploaded one)       │
│  Key spec badges                        │
├─────────────────────────────────────────┤
│  DESIGN PHILOSOPHY                      │
│  Quote + description text               │
├─────────────────────────────────────────┤
│  INTERNAL STRUCTURE                     │
│  SVG isometric cutaway illustration     │
│  Label callouts for key components      │
├─────────────────────────────────────────┤
│  EXPLODED VIEW (animated)               │
│  SVG components float apart on scroll   │
│  Auto-cycling or button-triggered       │
│  Labels + leader lines appear           │
├─────────────────────────────────────────┤
│  ORTHOGRAPHIC VIEWS                     │
│  SVG front / side / top / isometric     │
│  Dimension lines + measurements         │
├─────────────────────────────────────────┤
│  APP CONTROL (if applicable)            │
│  3 phone mockups with app UI            │
├─────────────────────────────────────────┤
│  FEATURES                               │
│  4-card grid with SVG icons + specs     │
├─────────────────────────────────────────┤
│  SPECIFICATIONS                         │
│  Spec table + SVG package drawing       │
├─────────────────────────────────────────┤
│  FOOTER                                 │
│  Copyright + philosophy statement       │
└─────────────────────────────────────────┘
```

> [!TIP]
> Not all sections are mandatory. For simpler products (e.g. a lamp), skip APP CONTROL. For non-electronic products, skip INTERNAL STRUCTURE and EXPLODED VIEW and show a materials/craftsmanship section instead.

### Phase 4: Design System Implementation

#### 4.1 HTML Boilerplate

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Brand] [Model] — [Tagline]</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
  <style>
    /* === DESIGN TOKENS === */
    :root {
      --color-bg: #FFFFFF;
      --color-bg-alt: #F8F8F8;
      --color-text: #1A1A1A;
      --color-text-secondary: #666666;
      --color-text-tertiary: #999999;
      --color-accent: #E85D2A;        /* ← from style preset */
      --color-accent-light: #FFF0EB;
      --color-border: #E5E5E5;
      --color-border-light: #F0F0F0;
      
      --font-primary: 'Inter', -apple-system, sans-serif;
      --font-mono: 'JetBrains Mono', 'SF Mono', monospace;
      
      --space-xs: 8px;
      --space-sm: 16px;
      --space-md: 24px;
      --space-lg: 48px;
      --space-xl: 80px;
      --space-2xl: 120px;
      
      --max-width: 1200px;
      --radius: 12px;
      --radius-lg: 20px;
      
      --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
  </style>
</head>
```

#### 4.2 Typography Scale

```css
/* Display — hero title */
.display { font-size: clamp(48px, 8vw, 96px); font-weight: 900; line-height: 1.0; letter-spacing: -0.03em; }

/* Heading 1 — section titles */
h1, .h1 { font-size: clamp(32px, 5vw, 56px); font-weight: 800; line-height: 1.1; letter-spacing: -0.02em; }

/* Heading 2 — subsection */
h2, .h2 { font-size: clamp(24px, 3vw, 36px); font-weight: 700; line-height: 1.2; }

/* Body large — descriptions */
.body-lg { font-size: 18px; line-height: 1.7; color: var(--color-text-secondary); }

/* Body — normal text */
.body { font-size: 16px; line-height: 1.6; }

/* Caption — labels, specs */
.caption { font-size: 13px; font-weight: 500; letter-spacing: 0.08em; text-transform: uppercase; color: var(--color-text-tertiary); }

/* Mono — technical values */
.mono { font-family: var(--font-mono); font-size: 14px; }
```

#### 4.3 Section Badge (the colored label above section titles)

```css
.section-badge {
  display: inline-block;
  padding: 6px 16px;
  border: 1.5px solid var(--color-accent);
  border-radius: 100px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-accent);
  margin-bottom: var(--space-md);
}
```

#### 4.4 Layout Patterns

```css
/* Full-width section with centered content */
.section {
  padding: var(--space-2xl) var(--space-lg);
  max-width: var(--max-width);
  margin: 0 auto;
}

/* Alternating background */
.section--alt { background: var(--color-bg-alt); }

/* Two-column layout (text left, visual right) */
.split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-xl);
  align-items: center;
}

/* Feature card grid */
.feature-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--space-md);
}
```

#### 4.5 Micro-Animations

```css
/* Fade-in on scroll (use IntersectionObserver) */
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Hover lift for cards */
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(0,0,0,0.08);
}

/* Accent underline animation */
.accent-line {
  width: 40px;
  height: 3px;
  background: var(--color-accent);
  transition: width 0.4s ease;
}
.card:hover .accent-line { width: 60px; }
```

#### 4.6 Scroll Reveal JavaScript

```javascript
// Add to bottom of HTML, before </body>
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

### Phase 5: Section-by-Section Implementation

#### 5.1 Navbar

```html
<nav class="navbar">
  <div class="nav-left">
    <span class="nav-brand">[BrandName]</span>
    <span class="nav-model caption">[Model]</span>
  </div>
  <div class="nav-links">
    <a href="#philosophy">Design Philosophy</a>
    <a href="#structure">Internal Structure</a>
    <a href="#views">Orthographic Views</a>
    <a href="#app">APP Control</a>
    <a href="#features">Features</a>
    <a href="#specs">Specifications</a>
  </div>
</nav>
```

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 40px;
  background: rgba(255,255,255,0.9);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--color-border-light);
}
.nav-brand { font-weight: 800; font-size: 20px; }
.nav-links a {
  font-size: 13px;
  color: var(--color-text-secondary);
  text-decoration: none;
  margin-left: 32px;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--color-text); }
```

#### 5.2 Hero Section

The hero section uses the **user-uploaded product image** as the centerpiece. The image should be embedded as base64 data URI or referenced from a relative path.

```html
<section class="hero">
  <div class="hero-content">
    <h1 class="display">[BrandName]</h1>
    <p class="hero-model mono">[Full Model String]</p>
    <p class="body-lg hero-desc">[2-3 sentence product description]</p>
    <div class="hero-badges">
      <span class="badge">[SPEC1]</span>
      <span class="badge">[SPEC2]</span>
      <span class="badge">[SPEC3]</span>
    </div>
  </div>
  <div class="hero-image">
    <img src="[product-image-path]" alt="[Product Name]">
  </div>
</section>
```

> [!IMPORTANT]
> The hero image is the ONLY raster image in the entire page. Everything else must be generated as inline SVG or HTML/CSS.

#### 5.3 Internal Structure / Cutaway SVG

This is the showpiece illustration. Create an **isometric cutaway view** that reveals internal components.

**SVG Construction Approach:**

1. Start with the outer shell as a 3D isometric box using parallelogram shapes
2. "Cut away" the front-left corner to reveal internals
3. Draw internal components aligned to the isometric grid
4. Use a muted color palette (grays, with accent color for key parts)
5. Add text labels with leader lines

**Isometric Grid Reference:**
- Isometric angles: 30° from horizontal
- X-axis: `transform="skewY(30)"` 
- Y-axis: `transform="skewY(-30)"`
- Use consistent unit grid (e.g., 10px = 1 unit)

```html
<section id="structure" class="section">
  <div class="section-header">
    <span class="section-badge">DESIGN PHILOSOPHY</span>
    <h1>Internal Structure. Meticulous.</h1>
    <p class="body-lg">Exquisite isometric cutaway illustration showcasing the product's precise internal structure</p>
  </div>
  <div class="structure-illustration">
    <svg viewBox="0 0 800 600" xmlns="http://www.w3.org/2000/svg">
      <!-- Outer shell (isometric box) -->
      <g class="shell">
        <!-- Top face -->
        <polygon points="400,100 650,225 400,350 150,225" fill="#F5F5F5" stroke="#333" stroke-width="1.5"/>
        <!-- Right face -->
        <polygon points="650,225 650,425 400,550 400,350" fill="#E8E8E8" stroke="#333" stroke-width="1.5"/>
        <!-- Left face (cutaway - partial) -->
        <polygon points="150,225 150,425 400,550 400,350" fill="#EFEFEF" stroke="#333" stroke-width="1.5"/>
      </g>
      
      <!-- Internal components -->
      <g class="internals">
        <!-- Transformer (example) -->
        <rect x="250" y="280" width="80" height="60" rx="4" fill="#F0F0F0" stroke="#666"/>
        <text x="290" y="315" text-anchor="middle" font-size="10" fill="#999">XFMR</text>
        
        <!-- Capacitors (example) -->
        <rect x="360" y="300" width="15" height="40" rx="2" fill="var(--color-accent)" opacity="0.8"/>
        <rect x="385" y="310" width="15" height="30" rx="2" fill="#4CAF50" opacity="0.8"/>
      </g>
      
      <!-- Label callouts -->
      <g class="labels">
        <line x1="290" y1="270" x2="200" y2="180" stroke="#999" stroke-dasharray="3"/>
        <text x="195" y="175" text-anchor="end" font-size="12" font-weight="500">Toroidal Transformer</text>
      </g>
    </svg>
  </div>
</section>
```

> [!TIP]
> **Key principle**: The SVG should reflect what you SEE in the product image. If you see knobs, draw knobs. If you see ventilation slots, draw those. Don't invent components that contradict the visible design.

#### 5.4 Animated Exploded View

This section shows the product **disassembled into its component parts**. Two visual styles are available — choose based on the desired aesthetic.

| Style | Approach | Best For | Output |
|-------|----------|----------|--------|
| **Photorealistic** (default) | `generate_image` from real product photo | Premium feel, product photography aesthetic | Static image(s) or multi-frame animation |
| **Schematic** | Inline SVG + CSS transitions | Interactive, code-only, no external tools | Auto-cycling CSS animation |

---

##### Style A: Photorealistic Exploded View (Recommended)

Uses the `generate_image` tool with the **original product image** as input to create a realistic 3D disassembly render.

**Workflow:**

1. **Analyze the product image** — identify 5-8 separable components (shell, controls, internals, base)
2. **Call `generate_image`** with the product photo, requesting a photorealistic exploded view
3. **Generate 1-3 views** at different angles (front vertical, 3/4 isometric, top-down)
4. **Embed the generated image(s)** in the page section

**Prompt Template for `generate_image`:**

```
Create a photorealistic 3D exploded view diagram of this [product type].
Show it disassembled into its component parts floating in space vertically,
with each part separated and aligned along a central vertical axis against
a clean white/light gray background.

From top to bottom, separate these components:
1) [top component] — [material description]
2) [second component] — [material description]
3) [third component] — [material description]
...
N) [base component] — [material description]

Each component should look like a real product render with realistic materials,
shadows, and reflections. Clean studio lighting, product photography style.
The components should be evenly spaced apart vertically to clearly show
each layer of the product's construction.
```

**Prompt Variants for Different Angles:**

| Angle | Add to Prompt |
|-------|--------------|
| Front vertical | "aligned along a central vertical axis" |
| 3/4 isometric | "viewed from a 3/4 top-down angle (about 45 degrees from above), along a diagonal axis" |
| Top-down | "viewed from directly above, components spread in a radial layout" |

**HTML Integration:**

```html
<section id="exploded" class="section">
  <div class="section-header">
    <span class="section-badge">ENGINEERING BREAKDOWN</span>
    <h1>Every Part. Purposeful.</h1>
    <p class="body-lg">[N] precision-engineered components, each designed for [purpose]</p>
  </div>
  <div class="exploded-image">
    <img src="[path-to-generated-exploded-view.png]" alt="Exploded view of [Product Name]">
  </div>
  <!-- Optional: component legend -->
  <div class="component-legend">
    <div class="legend-item"><span class="legend-num">01</span><span class="legend-name">[Component]</span><span class="legend-mat">[Material]</span></div>
    <!-- ... more items ... -->
  </div>
</section>
```

**Key Rules:**
- Always pass the **original product image** to `generate_image` — this ensures the output preserves the real product's shape, proportions, and materials
- Mention specific materials in the prompt (brushed aluminum, perforated steel, etc.) based on your Phase 1 image analysis
- Request "clean white/light gray background" to match the page aesthetic
- Generate at least 2 angles for variety (front vertical + isometric)

> [!IMPORTANT]
> The photorealistic style is the **default** for electronic and mechanical products. It produces the most convincing "product reveal" effect because the components look like real manufactured parts, not illustrations.

---

##### Style B: Schematic Exploded View (CSS-Animated SVG)

Uses **inline SVG components + CSS transitions** for a fully interactive, code-only exploded view that cycles between assembled and exploded states.

**Implementation Strategy:**

1. **Identify 5-8 major components** from the product image (e.g., outer shell, control knob, speaker driver, PCB, grille, base plate)
2. **Draw each as a separate SVG** inside its own `<div class="part">` positioned absolutely within a container
3. **Define two states via CSS classes**: assembled (default) and `.exploded` (components translated apart)
4. **Use CSS `transition` with staggered `transition-delay`** for sequential disassembly effect
5. **Trigger via IntersectionObserver** (scroll) AND/OR auto-cycling interval AND/OR manual button

**Container Structure:**

```html
<section id="exploded" class="section">
  <div class="section-header">
    <span class="section-badge">ENGINEERING BREAKDOWN</span>
    <h1>Every Part. Purposeful.</h1>
    <p class="body-lg">[N] precision-engineered components, each designed for [purpose]</p>
  </div>
  <div class="exploded-stage" id="explodedStage">
    <!-- Each part is absolutely positioned -->
    <div class="part part-knob">
      <svg viewBox="..."><!-- component SVG --></svg>
      <span class="part-label"><span class="leader"></span>Volume Knob<br><span class="part-material">CNC Stainless Steel</span></span>
    </div>
    <div class="part part-grille"><!-- ... --></div>
    <div class="part part-driver"><!-- ... --></div>
    <div class="part part-pcb"><!-- ... --></div>
    <div class="part part-shell"><!-- ghost outline --></div>
    <div class="part part-base"><!-- ... --></div>
  </div>
  <div class="exploded-controls">
    <button class="explode-btn" id="explodeBtn">EXPLODE</button>
    <button class="explode-btn auto-btn" id="autoBtn">AUTO ●</button>
  </div>
</section>
```

**Critical CSS:**

```css
.exploded-stage {
  position: relative;
  width: 600px;
  height: 560px;
  margin: 0 auto;
}

.part {
  position: absolute;
  left: 50%;
  /* Smooth elastic transition */
  transition: transform 1.2s cubic-bezier(0.22, 1, 0.36, 1),
              opacity 0.8s ease;
}

/* ASSEMBLED: each part at its "home" position */
.part-knob   { top: 50px;  width: 160px; z-index: 7; transform: translateX(-50%); }
.part-cap    { top: 95px;  width: 240px; z-index: 6; transform: translateX(-50%); }
.part-grille { top: 115px; width: 220px; z-index: 5; transform: translateX(-50%); }
.part-driver { top: 155px; width: 150px; z-index: 4; transform: translateX(-50%); }
.part-pcb    { top: 265px; width: 220px; z-index: 3; transform: translateX(-50%); }
.part-shell  { top: 100px; width: 260px; z-index: 2; transform: translateX(-50%); opacity: 0.8; }
.part-base   { top: 350px; width: 240px; z-index: 1; transform: translateX(-50%); }

/* EXPLODED: each part flies outward */
.exploded .part-knob   { transform: translateX(-50%) translateY(-100px); }
.exploded .part-cap    { transform: translateX(-50%) translateY(-55px); }
.exploded .part-grille { transform: translateX(-50%) translateX(120px) translateY(-15px) rotate(3deg); }
.exploded .part-driver { transform: translateX(-50%) translateX(-100px) translateY(15px) rotate(-3deg); }
.exploded .part-pcb    { transform: translateX(-50%) translateY(55px); }
.exploded .part-shell  { transform: translateX(-50%); opacity: 0.15; }
.exploded .part-base   { transform: translateX(-50%) translateY(100px); }

/* Stagger delays for sequential effect */
.part-knob   { transition-delay: 0.00s; }
.part-cap    { transition-delay: 0.06s; }
.part-grille { transition-delay: 0.12s; }
.part-driver { transition-delay: 0.18s; }
.part-pcb    { transition-delay: 0.24s; }
.part-shell  { transition-delay: 0.08s; }
.part-base   { transition-delay: 0.30s; }

/* Labels appear only when exploded */
.part-label {
  position: absolute;
  font-size: 11px;
  font-weight: 500;
  opacity: 0;
  transition: opacity 0.4s ease 0.9s;
  white-space: nowrap;
}
.part-material {
  color: var(--color-accent);
  font-size: 10px;
}
.exploded .part-label { opacity: 1; }
```

**JavaScript (dual-trigger: scroll + auto-cycle):**

```javascript
const stage = document.getElementById('explodedStage');
const btn = document.getElementById('explodeBtn');
let isExploded = false;
let autoInterval = null;

function toggleExplode() {
  isExploded = !isExploded;
  stage.classList.toggle('exploded', isExploded);
  btn.textContent = isExploded ? 'ASSEMBLE' : 'EXPLODE';
}

// Auto-cycle every 3 seconds
function startAuto() { autoInterval = setInterval(toggleExplode, 3000); }
function stopAuto()  { clearInterval(autoInterval); autoInterval = null; }

// Scroll trigger: explode when 40% visible
const explodedObserver = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting && e.intersectionRatio > 0.4 && !autoInterval) startAuto();
    if (!e.isIntersecting && autoInterval) { stopAuto(); if (isExploded) toggleExplode(); }
  });
}, { threshold: [0, 0.4] });

explodedObserver.observe(document.getElementById('exploded'));
btn.addEventListener('click', toggleExplode);
```

**SVG Component Drawing Rules (Schematic Style):**

| Component | SVG Approach | Key Details |
|-----------|-------------|-------------|
| Knob/Dial | Ellipses + vertical lines (knurl) | Use gradient fills for 3D depth |
| Top/Bottom Plate | Wide ellipse (disc shape) | Include mounting holes, port cutouts |
| Grille/Mesh | Rectangle with dot/line pattern | Use low-opacity circle grid for perforations |
| Speaker Driver | Concentric circles | Surround → cone → dust cap → magnet |
| PCB | Green rectangle with IC shapes + colored capacitor rectangles | Use `#1a7d4f` for PCB green |
| Body Shell | Dashed outline (goes transparent when exploded) | This becomes ghost/wireframe |
| Base Plate | Ellipse with rubber feet (dark circles) | Include port labels (USB-C, AUX, DC) |

> [!IMPORTANT]
> In schematic style, the body shell MUST use `stroke-dasharray` and become near-transparent (opacity 0.15) when exploded, so the internal components are visible in both states.

#### 5.5 Orthographic Views

Draw the product from 4 angles using precise, engineering-drawing aesthetics:

**View Configuration:**
```
┌──────────┬──────────┐
│ Front    │ Top      │
│ View     │ View     │
├──────────┼──────────┤
│ Side     │ Isometric│
│ View     │ View     │
└──────────┴──────────┘
```

**Drawing Conventions:**
- Visible edges: solid black lines, 1.5px stroke
- Hidden edges: dashed lines, 1px stroke, gray
- Dimension lines: thin red/accent lines with arrows and measurements
- Center lines: dash-dot pattern
- Fill: white or very light gray
- Feature details: buttons, ports drawn as simplified shapes

```html
<div class="ortho-grid">
  <!-- Front View -->
  <div class="ortho-view">
    <svg viewBox="0 0 300 200" xmlns="http://www.w3.org/2000/svg">
      <!-- Main outline -->
      <rect x="30" y="30" width="240" height="140" rx="4" fill="white" stroke="#1A1A1A" stroke-width="1.5"/>
      
      <!-- Features (buttons, display, ports - based on product image) -->
      <circle cx="80" cy="100" r="20" fill="none" stroke="#1A1A1A" stroke-width="1.5"/>
      <rect x="120" y="70" width="80" height="60" rx="2" fill="none" stroke="#1A1A1A" stroke-width="1"/>
      
      <!-- Dimension line -->
      <g class="dimension">
        <line x1="30" y1="185" x2="270" y2="185" stroke="var(--color-accent)" stroke-width="0.8"/>
        <line x1="30" y1="180" x2="30" y2="190" stroke="var(--color-accent)" stroke-width="0.8"/>
        <line x1="270" y1="180" x2="270" y2="190" stroke="var(--color-accent)" stroke-width="0.8"/>
        <text x="150" y="198" text-anchor="middle" font-size="11" fill="var(--color-accent)">480mm</text>
      </g>
    </svg>
    <p class="caption" style="text-align:center">Front View</p>
  </div>
  <!-- Repeat for Side, Top, Isometric views -->
</div>
```

**Legend (below the views):**
```html
<div class="ortho-legend">
  <span><span class="dot" style="background:var(--color-accent)"></span> Dimension Line</span>
  <span><span class="line-solid"></span> Outline</span>
  <span><span class="line-dashed"></span> Hidden Line</span>
  <span><span class="swatch" style="background:#1A1A1A"></span> Display</span>
</div>
```

#### 5.6 App Mockups

Build 3 complete phone screens using pure HTML/CSS:

```html
<div class="app-showcase">
  <!-- Phone 1: Main Control -->
  <div class="phone">
    <div class="phone-frame">
      <div class="phone-notch"></div>
      <div class="phone-screen">
        <div class="app-statusbar">
          <span>14:30</span>
          <div class="statusbar-icons">
            <span>■■■</span>
            <span>▪▪</span>
          </div>
        </div>
        <div class="app-content">
          <h3 class="app-title">[BrandName]</h3>
          <span class="app-status connected">● Connected</span>
          
          <!-- Big central display (e.g., VU meter, volume, temperature) -->
          <div class="app-meter">
            <span class="meter-value" style="color:var(--color-accent)">42</span>
            <span class="meter-unit">VU Level</span>
          </div>
          
          <!-- Input selector tabs -->
          <div class="app-tabs">
            <span>Input</span>
            <span class="tab-active">Line 1</span>
            <span>Line 2</span>
          </div>
        </div>
      </div>
      <div class="phone-home-indicator"></div>
    </div>
  </div>
  
  <!-- Phone 2: Analytics / Monitoring -->
  <!-- Phone 3: Settings -->
</div>
```

**Phone Frame CSS:**
```css
.phone-frame {
  width: 260px;
  height: 520px;
  background: #1A1A1A;
  border-radius: 36px;
  padding: 12px;
  box-shadow: 0 20px 60px rgba(0,0,0,0.15);
  position: relative;
}
.phone-screen {
  width: 100%;
  height: 100%;
  background: #FFFFFF;
  border-radius: 28px;
  overflow: hidden;
  padding: 16px;
}
.phone-notch {
  position: absolute;
  top: 12px;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 24px;
  background: #1A1A1A;
  border-radius: 0 0 16px 16px;
  z-index: 10;
}
.phone-home-indicator {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  width: 120px;
  height: 5px;
  background: #333;
  border-radius: 100px;
}
```

**App Screen Content Patterns:**

| Screen | Content | Key Visual |
|--------|---------|------------|
| Main Control | Device name, connection status, big metric, input selector | Large styled number/gauge |
| Analytics | Real-time spectrum, VU meter bars, THD+N / SNR readings | SVG bar chart + waveform |
| Settings | Device name, gain slider, capacitance buttons, firmware version | Form controls with accent colors |

#### 5.7 Features Grid

Four cards, each with an original SVG icon:

```html
<div class="feature-grid">
  <div class="feature-card card">
    <div class="feature-icon">
      <svg viewBox="0 0 64 64" width="64" height="64">
        <!-- Draw a unique icon that represents the feature -->
        <!-- Use consistent stroke-width (1.5-2px), no fill or minimal fill -->
        <!-- Match the product's geometric language -->
      </svg>
    </div>
    <h3 class="feature-name">[Feature Name]</h3>
    <p class="body feature-desc">[2-line description]</p>
    <div class="feature-specs">
      <span class="spec-highlight" style="color:var(--color-accent)">[Spec Label]</span>
      <span class="spec-value mono">[Spec Value]</span>
    </div>
    <div class="accent-line"></div>
  </div>
</div>
```

**Icon Design Rules:**
- ViewBox: `0 0 64 64`
- Stroke-width: 1.5px for main lines, 1px for details
- Style: line-art / outline only (no solid fills except accent highlights)
- Consistent corner radius and proportions across all 4 icons
- Each icon should be recognizably different from a distance

#### 5.8 Specifications Section

Two-column layout: spec table left, engineering drawing right.

```html
<section id="specs" class="section">
  <div class="specs-layout">
    <div class="specs-table">
      <h3 class="specs-category">Audio Performance</h3>
      <div class="spec-divider" style="background:var(--color-accent)"></div>
      <table>
        <tr><td class="spec-name">Output Power</td><td class="spec-val mono">2 × 100 W (8Ω)</td></tr>
        <tr><td class="spec-name">Frequency Response</td><td class="spec-val mono">20 Hz – 45 kHz (±0.5 dB)</td></tr>
        <!-- ... more rows ... -->
      </table>
      
      <h3 class="specs-category">Input/Output</h3>
      <div class="spec-divider"></div>
      <table>
        <!-- ... rows ... -->
      </table>
    </div>
    
    <div class="specs-drawings">
      <!-- Package dimension SVG -->
      <svg viewBox="0 0 400 500">
        <!-- 3D box outline with dimension lines -->
        <!-- Front face showing product label/logo -->
        <!-- Arrows and measurements -->
      </svg>
    </div>
  </div>
</section>
```

#### 5.9 Footer

Minimal, philosophical:

```html
<footer>
  <p>© [Brand] [Year] · Design follows Dieter Rams' ten principles</p>
  <p class="footer-sub">Form follows function · Less but better · Honesty in design</p>
  <p class="footer-sub">Virtual showcase, a tribute to classic industrial design</p>
</footer>
```

### Phase 6: Polish & Quality Checklist

Before delivering the final HTML, verify:

- [ ] **Single file**: All CSS is in `<style>`, all SVGs are inline, JS is in `<script>`. No external dependencies except Google Fonts.
- [ ] **Product image**: The uploaded image is referenced correctly (as base64 data URI or relative path).
- [ ] **SVG coherence**: All SVG illustrations reflect the actual product's shape, proportions, and features — not generic shapes.
- [ ] **Icon consistency**: All 4 feature icons use the same stroke-width, style, and viewBox.
- [ ] **Color system**: Exactly ONE accent color used throughout. All text colors use the design token vars.
- [ ] **Typography hierarchy**: Display > H1 > H2 > Body > Caption. No font-size values outside the system.
- [ ] **Responsive**: Works on viewport widths from 375px to 1920px (use `clamp()` and media queries).
- [ ] **Animations**: All `.reveal` elements have the IntersectionObserver attached. Hover effects work on cards.
- [ ] **No placeholder text**: All content is complete and plausible. Specs should have realistic numbers.
- [ ] **App mockups**: If included, each screen has a complete UI — not empty placeholders.
- [ ] **Page flow**: Sections tell a narrative story from hero (what) → philosophy (why) → structure (how) → features (details) → specs (precision).

### Adaptive Sections by Product Type

| Product Type | Include | Skip | Replace With |
|-------------|---------|------|-------------|
| Electronics (amp, speaker, etc.) | All sections incl. Exploded View | — | — |
| Furniture / Lighting | Hero, Philosophy, Views, Features, Specs | APP Control, Internal Structure, Exploded View | Materials & Craftsmanship |
| Wearable / Watch | Hero, Philosophy, Views, APP, Features, Specs | Internal Structure, Exploded View | On-Wrist Lifestyle section |
| Software / App | Hero, Philosophy, Features, Specs | Views, Internal Structure, Exploded View | Full screenshots + feature deep-dives |
| Kitchenware / Tools | Hero, Philosophy, Views, Features, Specs | APP, Internal Structure, Exploded View | In-Use / Process section |

### Advanced: Multi-Product Images

If the user provides multiple images of the same product (different angles), use them strategically:
- **Hero**: 3/4 perspective shot
- **Philosophy section**: Close-up detail shot
- **Features**: Additional angles showing specific features

### Output

Deliver a single `.html` file named `[brand]-[model]-official.html` (e.g., `soulrich-t100-official.html`). The file should:

1. Open directly in any modern browser with no server needed
2. Look production-ready at first glance
3. Be fully scrollable with smooth section transitions
4. Have all SVG illustrations rendering inline
5. Weigh under 500KB (excluding embedded product image)
