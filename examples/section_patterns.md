# Section Patterns — SVG, App Mockups, and CSS Reference

Ready-to-use patterns for each section type. Copy and adapt these to match the specific product.

---

## 1. SVG Orthographic Drawing Pattern

The key to convincing engineering drawings is **dimension lines** and **consistent stroke styles**.

### Dimension Line Component

```svg
<!-- Horizontal dimension line with measurement -->
<g class="dim-h">
  <!-- Extension lines (vertical ticks at each end) -->
  <line x1="30" y1="175" x2="30" y2="190" stroke="#E85D2A" stroke-width="0.75"/>
  <line x1="270" y1="175" x2="270" y2="190" stroke="#E85D2A" stroke-width="0.75"/>
  <!-- Main dimension line -->
  <line x1="30" y1="185" x2="270" y2="185" stroke="#E85D2A" stroke-width="0.75"/>
  <!-- Arrows (small triangles) -->
  <polygon points="30,185 36,182 36,188" fill="#E85D2A"/>
  <polygon points="270,185 264,182 264,188" fill="#E85D2A"/>
  <!-- Measurement text -->
  <text x="150" y="198" text-anchor="middle" font-family="Inter" font-size="11" fill="#E85D2A">480mm</text>
</g>

<!-- Vertical dimension line -->
<g class="dim-v">
  <line x1="285" y1="30" x2="295" y2="30" stroke="#E85D2A" stroke-width="0.75"/>
  <line x1="285" y1="170" x2="295" y2="170" stroke="#E85D2A" stroke-width="0.75"/>
  <line x1="290" y1="30" x2="290" y2="170" stroke="#E85D2A" stroke-width="0.75"/>
  <polygon points="290,30 287,36 293,36" fill="#E85D2A"/>
  <polygon points="290,170 287,164 293,164" fill="#E85D2A"/>
  <text x="300" y="105" font-family="Inter" font-size="11" fill="#E85D2A" transform="rotate(90, 300, 105)">110mm</text>
</g>
```

### Front View Template (Rect-ish product)

```svg
<svg viewBox="0 0 300 220" xmlns="http://www.w3.org/2000/svg" style="max-width:300px">
  <!-- Main body outline -->
  <rect x="30" y="30" width="240" height="140" rx="3" 
        fill="#FAFAFA" stroke="#1A1A1A" stroke-width="1.5"/>
  
  <!-- Panel details (knobs, buttons, display, vents) -->
  <!-- Adapt these to match the actual product -->
  
  <!-- Knob -->
  <circle cx="80" cy="100" r="22" fill="none" stroke="#1A1A1A" stroke-width="1.5"/>
  <circle cx="80" cy="100" r="16" fill="none" stroke="#999" stroke-width="0.5"/>
  <line x1="80" y1="78" x2="80" y2="84" stroke="#1A1A1A" stroke-width="2"/>
  
  <!-- Display/window -->
  <rect x="130" y="65" width="90" height="50" rx="2" 
        fill="#1A1A1A" stroke="#1A1A1A" stroke-width="1"/>
  
  <!-- Ventilation slots -->
  <g opacity="0.4">
    <line x1="50" y1="45" x2="110" y2="45" stroke="#666" stroke-width="0.8"/>
    <line x1="50" y1="49" x2="110" y2="49" stroke="#666" stroke-width="0.8"/>
    <line x1="50" y1="53" x2="110" y2="53" stroke="#666" stroke-width="0.8"/>
  </g>
  
  <!-- Hidden internal line (dashed) -->
  <rect x="60" y="100" width="180" height="40" rx="2"
        fill="none" stroke="#999" stroke-width="0.8" stroke-dasharray="4,3"/>
  
  <!-- Dimensions -->
  <line x1="30" y1="185" x2="270" y2="185" stroke="#E85D2A" stroke-width="0.75"/>
  <text x="150" y="200" text-anchor="middle" font-size="11" fill="#E85D2A">480mm</text>
</svg>
```

### Side View Template

```svg
<svg viewBox="0 0 200 220" xmlns="http://www.w3.org/2000/svg" style="max-width:200px">
  <!-- Main body (narrower from side) -->
  <rect x="40" y="30" width="120" height="140" rx="3"
        fill="#FAFAFA" stroke="#1A1A1A" stroke-width="1.5"/>
  
  <!-- Back panel ports (if visible from side, draw small rectangles) -->
  <rect x="155" y="60" width="5" height="12" fill="#333"/>
  <rect x="155" y="80" width="5" height="12" fill="#333"/>
  <rect x="155" y="100" width="5" height="12" fill="#333"/>
  
  <!-- Ventilation (side) -->
  <g opacity="0.3">
    <line x1="60" y1="50" x2="60" y2="150" stroke="#666" stroke-width="0.5"/>
    <line x1="65" y1="50" x2="65" y2="150" stroke="#666" stroke-width="0.5"/>
  </g>
</svg>
```

---

## 2. Isometric Box Construction

Build a 3D product view using three parallelogram faces:

```svg
<svg viewBox="0 0 400 350" xmlns="http://www.w3.org/2000/svg">
  <!-- Isometric box: W=200, H=100, D=150 -->
  <!-- Reference point: front-bottom-left at (80, 280) -->
  
  <!-- Top face (lightest) -->
  <polygon points="80,180 230,105 380,180 230,255" 
           fill="#F0F0F0" stroke="#333" stroke-width="1.5"/>
  
  <!-- Right face (medium) -->
  <polygon points="380,180 380,280 230,355 230,255" 
           fill="#E0E0E0" stroke="#333" stroke-width="1.5"/>
  
  <!-- Left face (medium-dark for depth) -->
  <polygon points="80,180 80,280 230,355 230,255" 
           fill="#E8E8E8" stroke="#333" stroke-width="1.5"/>
  
  <!-- Brand text on front face -->
  <text x="155" y="300" font-family="Inter" font-weight="700" font-size="16" 
        transform="skewY(30)" fill="#333">BrandName</text>
  
  <!-- LED indicator on top -->
  <circle cx="180" cy="165" r="4" fill="#4CAF50"/>
</svg>
```

**Isometric Angle Cheat Sheet:**
- Move **right** on X-axis: `(+2, +1)` per unit
- Move **left** on Y-axis: `(-2, +1)` per unit
- Move **up** on Z-axis: `(0, -1)` per unit

---

## 3. Phone Mockup Complete Pattern

### Frame CSS

```css
.phone-showcase {
  display: flex;
  justify-content: center;
  gap: 40px;
  padding: 60px 0;
}

.phone {
  flex-shrink: 0;
}

.phone-frame {
  width: 260px;
  height: 530px;
  background: #1A1A1A;
  border-radius: 40px;
  padding: 10px;
  position: relative;
  box-shadow: 
    0 30px 80px rgba(0,0,0,0.12),
    inset 0 0 0 1px rgba(255,255,255,0.05);
}

.phone-screen {
  width: 100%;
  height: 100%;
  background: #fff;
  border-radius: 32px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

/* Dynamic Island style notch */
.phone-notch {
  position: absolute;
  top: 16px;
  left: 50%;
  transform: translateX(-50%);
  width: 90px;
  height: 22px;
  background: #1A1A1A;
  border-radius: 20px;
  z-index: 10;
}

.phone-home-bar {
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  width: 110px;
  height: 4px;
  background: #444;
  border-radius: 4px;
}
```

### Status Bar Pattern

```html
<div class="app-statusbar" style="
  display: flex; justify-content: space-between; align-items: center;
  padding: 14px 20px 8px; font-size: 12px; font-weight: 600;
">
  <span>14:30</span>
  <div style="display:flex; gap:4px; align-items:center;">
    <!-- Signal bars -->
    <svg width="16" height="12" viewBox="0 0 16 12">
      <rect x="0" y="8" width="3" height="4" rx="0.5" fill="#1A1A1A"/>
      <rect x="4.5" y="5" width="3" height="7" rx="0.5" fill="#1A1A1A"/>
      <rect x="9" y="2" width="3" height="10" rx="0.5" fill="#1A1A1A"/>
      <rect x="13.5" y="0" width="3" height="12" rx="0.5" fill="#C0C0C0"/>
    </svg>
    <!-- WiFi -->
    <svg width="14" height="12" viewBox="0 0 14 12">
      <path d="M7,10 L5,7 C5.8,6.2 6.4,5.8 7,5.8 C7.6,5.8 8.2,6.2 9,7 Z" fill="#1A1A1A"/>
      <path d="M7,7 L3,3 C4.5,1.5 6,1 7,1 C8,1 9.5,1.5 11,3 Z" fill="#1A1A1A" opacity="0.5"/>
    </svg>
    <!-- Battery -->
    <svg width="22" height="12" viewBox="0 0 22 12">
      <rect x="0" y="1" width="19" height="10" rx="2" fill="none" stroke="#1A1A1A" stroke-width="1"/>
      <rect x="2" y="3" width="14" height="6" rx="1" fill="#1A1A1A"/>
      <rect x="20" y="4" width="2" height="4" rx="0.5" fill="#1A1A1A"/>
    </svg>
  </div>
</div>
```

### App Screen 1: Main Control

```html
<div class="app-main" style="padding: 0 20px; flex: 1; display: flex; flex-direction: column;">
  <div style="display:flex; justify-content:space-between; align-items:center; margin-top:10px;">
    <div>
      <div style="font-weight:700; font-size:18px;">BrandName</div>
      <div style="font-size:11px; color:#4CAF50;">● Connected</div>
    </div>
    <svg width="24" height="24" viewBox="0 0 24 24">
      <rect x="3" y="3" width="7" height="7" rx="1.5" fill="#333"/>
      <rect x="14" y="3" width="7" height="7" rx="1.5" fill="#333"/>
      <rect x="3" y="14" width="7" height="7" rx="1.5" fill="#333"/>
      <rect x="14" y="14" width="7" height="7" rx="1.5" fill="#333"/>
    </svg>
  </div>
  
  <!-- Big central metric -->
  <div style="flex:1; display:flex; flex-direction:column; align-items:center; justify-content:center;">
    <div style="
      width: 140px; height: 140px; border-radius: 50%;
      background: linear-gradient(135deg, #FF6B35, #E85D2A);
      display: flex; align-items: center; justify-content: center;
      box-shadow: 0 8px 30px rgba(232,93,42,0.3);
    ">
      <span style="font-size:48px; font-weight:800; color:white;">42</span>
    </div>
    <span style="margin-top:12px; font-size:13px; color:#999; letter-spacing:0.05em;">VU LEVEL</span>
  </div>
  
  <!-- Input selector -->
  <div style="
    display:flex; background:#F5F5F5; border-radius:12px; padding:4px; margin-bottom:20px;
  ">
    <div style="padding:8px 0; flex:1; text-align:center; font-size:12px; color:#999;">Input</div>
    <div style="padding:8px 0; flex:1; text-align:center; font-size:12px; background:white; border-radius:10px; font-weight:600; box-shadow:0 1px 4px rgba(0,0,0,0.08);">Line 1</div>
    <div style="padding:8px 0; flex:1; text-align:center; font-size:12px; color:#999;">Line 2</div>
  </div>
</div>
```

### App Screen 2: Analytics / Spectrum

```html
<div class="app-analytics" style="padding: 0 20px; flex: 1;">
  <h3 style="font-size:18px; font-weight:700; margin-top:12px;">Audio Analysis</h3>
  <p style="font-size:12px; color:#666; margin-top:2px;">Real-time Spectrum</p>
  
  <!-- Spectrum bars -->
  <div style="display:flex; gap:3px; align-items:flex-end; height:80px; margin-top:20px;">
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:45%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:70%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:90%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:60%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:35%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:50%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:25%;"></div>
    <div style="flex:1; background: linear-gradient(to top, #E85D2A, #FF8A5C); border-radius:3px 3px 0 0; height:15%;"></div>
  </div>
  
  <div style="display:flex; gap:20px; margin-top:24px;">
    <!-- THD+N reading -->
    <div>
      <div style="font-size:11px; color:#999;">THD+N</div>
      <div style="font-size:28px; font-weight:700;">0.003<span style="font-size:14px; color:#999;">%</span></div>
    </div>
    <!-- SNR reading -->
    <div>
      <div style="font-size:11px; color:#999;">SNR</div>
      <div style="font-size:28px; font-weight:700;">118<span style="font-size:14px; color:#999;"> dB</span></div>
    </div>
  </div>
</div>
```

### App Screen 3: Settings

```html
<div class="app-settings" style="padding: 0 20px; flex: 1;">
  <h3 style="font-size:18px; font-weight:700; margin-top:12px;">Settings</h3>
  
  <!-- Settings rows -->
  <div style="margin-top:16px;">
    <div style="display:flex; justify-content:space-between; padding:12px 0; border-bottom:1px solid #F0F0F0;">
      <span style="font-size:14px;">Device Name</span>
      <span style="font-size:14px; color:#999;">Living Room</span>
    </div>
    <div style="display:flex; justify-content:space-between; align-items:center; padding:12px 0; border-bottom:1px solid #F0F0F0;">
      <span style="font-size:14px;">Phono Gain</span>
      <span style="font-size:14px; color:#E85D2A; font-weight:600;">42 dB</span>
    </div>
    
    <!-- Capacitance selector (chip buttons) -->
    <div style="padding:12px 0; border-bottom:1px solid #F0F0F0;">
      <span style="font-size:14px;">Phono Capacitance</span>
      <div style="display:flex; gap:8px; margin-top:8px;">
        <span style="padding:4px 12px; background:#F5F5F5; border-radius:6px; font-size:12px;">100</span>
        <span style="padding:4px 12px; background:#E85D2A; color:white; border-radius:6px; font-size:12px; font-weight:600;">220</span>
        <span style="padding:4px 12px; background:#F5F5F5; border-radius:6px; font-size:12px;">330</span>
      </div>
    </div>
    
    <div style="display:flex; justify-content:space-between; padding:12px 0; border-bottom:1px solid #F0F0F0;">
      <span style="font-size:14px;">Firmware Version</span>
      <span style="font-size:14px; color:#999; font-family:monospace;">v2.1.4</span>
    </div>
    <div style="display:flex; justify-content:space-between; padding:12px 0;">
      <span style="font-size:14px;">About</span>
      <span style="font-size:14px; color:#CCC;">›</span>
    </div>
  </div>
</div>
```

---

## 4. Feature Card with SVG Icon Pattern

### Complete Card HTML

```html
<div class="feature-card" style="
  padding: 32px;
  background: #FAFAFA;
  border-radius: 16px;
  transition: all 0.3s ease;
  cursor: default;
">
  <!-- Icon -->
  <div style="width:64px; height:64px; margin-bottom:24px;">
    <svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
      <!-- Example: Speaker/Audio icon -->
      <rect x="8" y="16" width="48" height="32" rx="4" stroke="#1A1A1A" stroke-width="1.5"/>
      <circle cx="24" cy="32" r="8" stroke="#1A1A1A" stroke-width="1.5"/>
      <circle cx="24" cy="32" r="3" fill="#1A1A1A"/>
      <circle cx="44" cy="32" r="6" stroke="#1A1A1A" stroke-width="1.5"/>
      <line x1="44" y1="26" x2="44" y2="28" stroke="#1A1A1A" stroke-width="2" stroke-linecap="round"/>
    </svg>
  </div>
  
  <!-- Title -->
  <h3 style="font-size:18px; font-weight:700; margin-bottom:8px;">Analog Phono Stage</h3>
  
  <!-- Description -->
  <p style="font-size:14px; line-height:1.6; color:#666; margin-bottom:16px;">
    Fully discrete low-noise amplification, precisely restoring every groove detail from vinyl records.
  </p>
  
  <!-- Spec highlights -->
  <div>
    <div style="color:#E85D2A; font-size:13px; font-weight:500; margin-bottom:4px;">Noise: &lt; 0.3μV</div>
    <div style="color:#E85D2A; font-size:13px; font-weight:500;">RIAA Error: &lt; 0.1dB</div>
  </div>
  
  <!-- Accent line -->
  <div style="width:40px; height:3px; background:#E85D2A; margin-top:20px; border-radius:2px; transition: width 0.3s;"></div>
</div>
```

### Icon Design Cheat Sheet

All icons should follow these rules:
- **ViewBox**: `0 0 64 64`
- **Stroke**: `#1A1A1A`, width `1.5px`
- **Fill**: `none` (outline style) or minimal accent fills
- **Corner Radius**: `rx="3"` or `rx="4"` for rectangles
- **Line Cap**: `round` for line endpoints
- **Style**: Clean, geometric, recognizable at 32x32px

Common icon compositions:

| Feature | Icon Approach |
|---------|--------------|
| Volume/Knob | Concentric circles + position indicator line |
| Protection | Shield shape or circuit breaker symbol |
| Connectivity | WiFi arcs or Bluetooth symbol |
| Ports/IO | Rectangle array with different sized openings |
| Power | Circle + vertical line (power symbol) |
| Frequency | Sine wave path |
| Display | Rounded rectangle with content lines |
| Speaker | Cone + sound wave arcs |

---

## 5. Specification Table Pattern

```html
<div style="max-width:500px;">
  <!-- Category header -->
  <h3 style="font-size:16px; font-weight:700; margin-bottom:8px;">Audio Performance</h3>
  <div style="height:3px; background:#E85D2A; width:40px; margin-bottom:16px; border-radius:2px;"></div>
  
  <!-- Spec rows -->
  <div style="display:flex; justify-content:space-between; padding:12px 0; border-bottom:1px solid #F0F0F0;">
    <span style="font-size:14px; color:#333;">Output Power</span>
    <span style="font-size:14px; font-family:'JetBrains Mono',monospace; color:#666;">2 × 100 W (8Ω)</span>
  </div>
  <div style="display:flex; justify-content:space-between; padding:12px 0; border-bottom:1px solid #F0F0F0;">
    <span style="font-size:14px; color:#333;">Frequency Response</span>
    <span style="font-size:14px; font-family:'JetBrains Mono',monospace; color:#666;">20 Hz – 45 kHz (±0.5 dB)</span>
  </div>
  <div style="display:flex; justify-content:space-between; padding:12px 0; border-bottom:1px solid #F0F0F0;">
    <span style="font-size:14px; color:#333;">Input Impedance</span>
    <span style="font-size:14px; font-family:'JetBrains Mono',monospace; color:#666;">47 kΩ</span>
  </div>
  <!-- ... more rows ... -->
</div>
```

---

## 6. Package Dimension Drawing

```svg
<svg viewBox="0 0 400 300" xmlns="http://www.w3.org/2000/svg">
  <!-- 3D box -->
  <!-- Bottom face (top-down perspective) -->
  <polygon points="80,100 280,100 320,80 120,80" fill="#F8F8F8" stroke="#333" stroke-width="1"/>
  <!-- Front face -->
  <rect x="80" y="100" width="200" height="140" fill="white" stroke="#333" stroke-width="1.5"/>
  <!-- Side face -->
  <polygon points="280,100 320,80 320,220 280,240" fill="#EFEFEF" stroke="#333" stroke-width="1"/>
  
  <!-- Product label on front -->
  <text x="180" y="170" text-anchor="middle" font-family="Inter" font-weight="700" font-size="14" fill="#333">BrandName</text>
  <text x="180" y="188" text-anchor="middle" font-family="'JetBrains Mono'" font-size="10" fill="#999">Model T-100</text>
  
  <!-- Width dimension -->
  <line x1="80" y1="260" x2="280" y2="260" stroke="#E85D2A" stroke-width="0.75"/>
  <text x="180" y="275" text-anchor="middle" font-size="11" fill="#E85D2A">530mm</text>
  
  <!-- Package contents strip (below) -->
  <rect x="60" y="285" width="280" height="1" fill="#E5E5E5"/>
  <text x="65" y="298" font-size="9" fill="#999">Package Elements</text>
  <rect x="80" y="290" width="50" height="2" fill="#CCC"/>
  <rect x="140" y="290" width="50" height="2" fill="#CCC"/>
  <rect x="200" y="290" width="50" height="2" fill="#CCC"/>
  <rect x="260" y="290" width="50" height="2" fill="#CCC"/>
</svg>
```

---

## 7. Responsive Breakpoints

```css
/* Tablet (768px) */
@media (max-width: 768px) {
  .split { grid-template-columns: 1fr; }
  .feature-grid { grid-template-columns: repeat(2, 1fr); }
  .phone-showcase { flex-direction: column; align-items: center; }
  .ortho-grid { grid-template-columns: repeat(2, 1fr); }
  .specs-layout { grid-template-columns: 1fr; }
}

/* Mobile (480px) */
@media (max-width: 480px) {
  .feature-grid { grid-template-columns: 1fr; }
  .ortho-grid { grid-template-columns: 1fr; }
  .navbar { padding: 12px 20px; }
  .nav-links { display: none; }
  .section { padding: 60px 20px; }
}
```

---

## 8. Smooth Scroll + Active Nav

```javascript
// Smooth scroll for nav links
document.querySelectorAll('.nav-links a').forEach(link => {
  link.addEventListener('click', (e) => {
    e.preventDefault();
    const target = document.querySelector(link.getAttribute('href'));
    if (target) {
      target.scrollIntoView({ behavior: 'smooth', block: 'start' });
    }
  });
});

// Highlight active nav link on scroll
const sections = document.querySelectorAll('section[id]');
const navLinks = document.querySelectorAll('.nav-links a');

window.addEventListener('scroll', () => {
  let current = '';
  sections.forEach(section => {
    const sectionTop = section.offsetTop - 100;
    if (scrollY >= sectionTop) {
      current = section.getAttribute('id');
    }
  });
  navLinks.forEach(link => {
    link.style.color = link.getAttribute('href') === '#' + current 
      ? '#1A1A1A' 
      : '#999';
    link.style.fontWeight = link.getAttribute('href') === '#' + current 
      ? '600' 
      : '400';
  });
});
```
