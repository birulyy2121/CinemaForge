---
name: cinemaforge
description: Use when creating professional motion graphics, product launch videos, SaaS ads, kinetic typography, animated reveals, or any video requiring After-Effects-grade polish via code. Use for HyperFrames or Remotion output with spring physics, custom easing, beat-synced transitions, and agency-tier visual design.
---

# CinemaForge — Professional Motion Graphics for AI Agents

> After-Effects-grade motion design, authored entirely in code.

CinemaForge teaches AI agents to produce **AAA-tier motion graphics** — the kind of work that looks like a professional motion designer built it in After Effects with days of polish. It targets **HyperFrames** (HTML/GSAP) and **Remotion** (React) as render backends.

## Overview

CinemaForge encodes the complete discipline of professional motion design into executable rules:

1. **Physics-based easing** — spring dynamics, cubic-bezier curves, overshoot/settle
2. **The 12 Principles of Animation** applied to motion graphics
3. **Scene architecture** — hook → build → reveal → resolve narrative arcs
4. **Beat-synced timing** — transitions land on musical/rhythmic beats
5. **Typography as motion** — kinetic type that communicates through movement
6. **Component library** — phone mockups, UI windows, dashboard cards, charts, data viz
7. **Color & light** — dark-mode-first palettes, accent glow, grain textures, glassmorphism
8. **Export pipeline** — 4K 60fps with 4× subframe motion blur

## When to Use

- Building a **product launch video** or **SaaS ad**
- Creating **kinetic typography** sequences
- Designing **animated UI/UX showcases** or **feature reveals**
- Making **social media motion graphics** (Reels, Shorts, LinkedIn)
- Producing **brand anthem / manifesto videos**
- Building **data visualization animations**
- Any project where the motion must feel **hand-crafted, not templated**

## When NOT to Use

- Simple slide decks or static presentations → use `slides` skill
- Talking-head video editing → use `edit` skill
- AI-generated imagery → use `image-generator`
- Pure audio/music work → use `sound` skill

---

## Core Philosophy: The CinemaForge Standard

### The Three Laws

1. **Nothing moves linearly.** Every property change uses physics-based or custom-bezier easing. Linear motion is banned.
2. **Nothing appears without motivation.** Every element enters with anticipation, moves with purpose, and settles with follow-through.
3. **Nothing exists in isolation.** Every element's motion relates to its neighbors through staggered timing, shared rhythm, and spatial hierarchy.

### The Quality Bar

A CinemaForge video must pass the **"Agency Test"**: if a viewer cannot tell whether a human motion designer or an AI agent made it, the standard is met. If it looks "AI-generated" or "templated," it fails.

---

## Scene Architecture

Every CinemaForge video follows a **narrative motion arc** — not a random sequence of effects, but a deliberate dramatic structure.

### The Four-Act Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  ACT 1: HOOK          │  0–3 seconds                           │
│  ─────────────────────│────────────────────────────────────────│
│  Purpose:             │  Stop the scroll. Create tension.       │
│  Motion style:        │  Sharp, fast, high-contrast.           │
│  Elements:            │  Bold typography, visual disruption.    │
│  Easing:              │  Aggressive ease-out, snap-in.         │
├─────────────────────────────────────────────────────────────────┤
│  ACT 2: BUILD         │  3–12 seconds                          │
│  ─────────────────────│────────────────────────────────────────│
│  Purpose:             │  Establish context, present problem.    │
│  Motion style:        │  Rhythmic, structured, progressive.     │
│  Elements:            │  Staggered reveals, data points, UI.    │
│  Easing:              │  Smooth power3/power4, gentle springs.  │
├─────────────────────────────────────────────────────────────────┤
│  ACT 3: REVEAL        │  12–22 seconds                         │
│  ─────────────────────│────────────────────────────────────────│
│  Purpose:             │  Showcase the product/solution.         │
│  Motion style:        │  Cinematic, expansive, impressive.      │
│  Elements:            │  Product UI, 3D mockups, feature cards. │
│  Easing:              │  Lush springs with overshoot, arcs.     │
├─────────────────────────────────────────────────────────────────┤
│  ACT 4: RESOLVE       │  22–30 seconds                         │
│  ─────────────────────│────────────────────────────────────────│
│  Purpose:             │  Call to action, brand lock-up.          │
│  Motion style:        │  Settling, confident, final.            │
│  Elements:            │  Logo, tagline, URL, CTA button.        │
│  Easing:              │  Underdamped spring settle, fade.       │
└─────────────────────────────────────────────────────────────────┘
```

### Section Timing Rules

| Duration | Use Case | Pacing |
|----------|----------|--------|
| 15 sec   | Instagram Story ad | 2-2-8-3 split |
| 30 sec   | Standard product ad | 3-9-12-6 split |
| 60 sec   | Full explainer | 5-20-25-10 split |
| 90 sec   | Deep feature showcase | 8-30-35-17 split |

---

## The Physics Engine: Easing & Springs

### BANNED: Linear Motion

```javascript
// ❌ NEVER — robotic, cheap, amateur
gsap.to(el, { x: 500, duration: 1, ease: "none" });

// ❌ NEVER — default ease is not enough
gsap.to(el, { x: 500, duration: 1 });
```

### Required: Physics-Based Easing

Every motion must use one of these easing systems:

#### 1. Custom Cubic-Bezier Curves

```javascript
// The CinemaForge Signature Curves
const CF_EASE = {
  // Snap-in: aggressive deceleration (hook entries)
  snapIn:    "cubic-bezier(0.16, 1, 0.3, 1)",      // gsap: CustomEase
  
  // Smooth-out: elegant departure (exit transitions)  
  smoothOut: "cubic-bezier(0.55, 0, 0.1, 1)",
  
  // Punch: fast attack, soft settle (feature reveals)
  punch:     "cubic-bezier(0.22, 1, 0.36, 1)",
  
  // Glide: smooth symmetrical (ambient motion)
  glide:     "cubic-bezier(0.25, 0.1, 0.25, 1)",
  
  // Whip: extreme acceleration for fast cuts
  whip:      "cubic-bezier(0.9, 0, 0.1, 1)",
};

// GSAP equivalents for each
const CF_GSAP = {
  snapIn:    "power4.out",
  smoothOut: "power2.inOut",
  punch:     "power3.out",
  glide:     "power1.inOut",
  whip:      "expo.inOut",
};
```

#### 2. Spring Physics (Damped Harmonic Oscillator)

```javascript
/**
 * CinemaForge Spring — deterministic, seekable, no libraries needed.
 * 
 * @param {number} t      - Current time in seconds since trigger
 * @param {number} from   - Start value
 * @param {number} to     - Target value
 * @param {Object} config - { tension, friction, mass }
 * @returns {number}      - Interpolated value at time t
 */
function cfSpring(t, from, to, config = {}) {
  const { tension = 170, friction = 26, mass = 1 } = config;
  
  const omega0 = Math.sqrt(tension / mass);
  const zeta = friction / (2 * Math.sqrt(tension * mass));
  
  const amplitude = to - from;
  let value;
  
  if (zeta < 1) {
    // Underdamped — bouncy, alive, premium feel
    const omegaD = omega0 * Math.sqrt(1 - zeta * zeta);
    const decay = Math.exp(-zeta * omega0 * t);
    value = to - amplitude * decay * (
      Math.cos(omegaD * t) + 
      (zeta * omega0 / omegaD) * Math.sin(omegaD * t)
    );
  } else if (zeta === 1) {
    // Critically damped — smooth, no bounce
    const decay = Math.exp(-omega0 * t);
    value = to - amplitude * decay * (1 + omega0 * t);
  } else {
    // Overdamped — slow, heavy, deliberate
    const s1 = -omega0 * (zeta + Math.sqrt(zeta * zeta - 1));
    const s2 = -omega0 * (zeta - Math.sqrt(zeta * zeta - 1));
    value = to - amplitude * (
      (s2 * Math.exp(s1 * t) - s1 * Math.exp(s2 * t)) / (s2 - s1)
    );
  }
  
  return value;
}

// Preset spring configs for different motion characters
const CF_SPRINGS = {
  // Snappy UI elements, quick reveals
  snappy:   { tension: 300, friction: 20, mass: 1 },
  
  // Bouncy entries, playful feel
  bouncy:   { tension: 180, friction: 12, mass: 1 },
  
  // Smooth settle, premium product reveals  
  gentle:   { tension: 120, friction: 26, mass: 1 },
  
  // Heavy, cinematic camera moves
  heavy:    { tension: 80,  friction: 30, mass: 2 },
  
  // Elastic overshoot, attention-grabbing
  elastic:  { tension: 200, friction: 10, mass: 1 },
  
  // Slow, luxurious reveals
  molasses: { tension: 60,  friction: 40, mass: 3 },
};
```

#### 3. Overshoot & Settle Pattern

```javascript
/**
 * Overshoot — element goes PAST target then settles back.
 * This is the #1 technique that separates amateur from professional.
 */
function cfOvershoot(progress, overshootAmount = 0.15) {
  // progress: 0 → 1
  if (progress < 0.7) {
    // Fast attack to target + overshoot
    const t = progress / 0.7;
    return t * t * (1 + overshootAmount);
  } else {
    // Settle back from overshoot to 1.0
    const t = (progress - 0.7) / 0.3;
    const overshootValue = 1 + overshootAmount;
    return overshootValue + (1 - overshootValue) * (t * t * (3 - 2 * t));
  }
}

// In GSAP: use back.out for overshoot
gsap.to(el, { 
  scale: 1, 
  duration: 0.8, 
  ease: "back.out(1.7)"  // 1.7 = overshoot intensity
});
```

---

## The 12 Principles Applied to Motion Graphics

Every CinemaForge composition must demonstrate mastery of these principles:

### Mandatory Principles (use in EVERY video)

| Principle | Motion Graphics Application | Implementation |
|-----------|---------------------------|----------------|
| **Easing** (Slow In/Out) | Custom curves on ALL motion | `power3.out`, `power4.out`, spring physics |
| **Anticipation** | Micro-pullback before major moves | Scale down 5% for 3 frames before scaling up |
| **Follow-Through** | Elements continue past target, settle | Staggered child stops, trailing elements |
| **Staging** | One hero element at a time | Dim/blur non-focus elements, sequence reveals |
| **Timing** | Speed = personality of the brand | Fast = tech/startup; Slow = luxury/premium |
| **Appeal** | Clean hierarchy, premium palette | Dark mode, accent colors, proper type scale |

### Situational Principles (use when appropriate)

| Principle | When to Apply | Implementation |
|-----------|--------------|----------------|
| **Squash & Stretch** | Playful brands, bouncy UI | Scale X/Y inversely on impact |
| **Exaggeration** | Hero moments, feature reveals | 120% scale on entrance, then settle to 100% |
| **Arcs** | Spatial transitions, floating elements | Bezier motion paths instead of linear |
| **Secondary Action** | Complex scenes, dashboard reveals | Shadow expansion, gradient shift, icon fade |
| **Overlapping** | Multi-element compositions | 2–4 frame stagger between children |
| **Solid Drawing** | 3D mockups, perspective cards | Consistent vanishing point, light direction |

---

## Kinetic Typography System

Typography is the backbone of motion graphics. CinemaForge defines a complete typographic motion system.

### Type Hierarchy

```
┌──────────────────────────────────────────────┐
│  DISPLAY    │  48–120px  │  Impact moments    │
│  HEADLINE   │  32–48px   │  Section titles    │
│  SUBHEAD    │  24–32px   │  Feature labels    │
│  BODY       │  16–20px   │  Descriptions      │
│  CAPTION    │  12–14px   │  Metadata, labels  │
│  METRIC     │  64–200px  │  Big numbers       │
└──────────────────────────────────────────────┘
```

### Font Stack (by brand personality)

| Personality | Primary | Mono | Weight Range |
|------------|---------|------|-------------|
| **Tech / Startup** | Inter, Geist Sans | Geist Mono, JetBrains Mono | 400–800 |
| **Premium / Luxury** | Satoshi, General Sans | Space Mono | 300–700 |
| **Editorial / Media** | Instrument Serif, Playfair | IBM Plex Mono | 300–900 |
| **Corporate / Enterprise** | Plus Jakarta Sans | Source Code Pro | 400–700 |
| **Creative / Agency** | Clash Display, Cabinet Grotesk | Fira Code | 500–900 |

### Text Entry Animations

```javascript
// 1. CHARACTER CASCADE — letters arrive one by one
function charCascade(el, { stagger = 0.03, ease = "power3.out" } = {}) {
  // Split text into individual characters
  const chars = el.textContent.split('');
  el.innerHTML = chars.map(c => 
    c === ' ' ? ' ' : `<span class="cf-char">${c}</span>`
  ).join('');
  
  return gsap.from('.cf-char', {
    y: 40,
    opacity: 0,
    duration: 0.6,
    stagger: stagger,
    ease: ease,
  });
}

// 2. WORD PUNCH — words slam in beat-synced
function wordPunch(el, { stagger = 0.08 } = {}) {
  const words = el.textContent.split(' ');
  el.innerHTML = words.map(w => 
    `<span class="cf-word">${w}</span>`
  ).join(' ');
  
  return gsap.from('.cf-word', {
    scale: 1.5,
    opacity: 0,
    y: -20,
    duration: 0.4,
    stagger: stagger,
    ease: "back.out(2)",
  });
}

// 3. LINE WIPE — text reveals behind a traveling mask
function lineWipe(el, { direction = 'left' } = {}) {
  return gsap.timeline()
    .set(el, { clipPath: 'inset(0 100% 0 0)' })
    .to(el, { 
      clipPath: 'inset(0 0% 0 0)', 
      duration: 0.8, 
      ease: "power4.inOut" 
    });
}

// 4. METRIC COUNTER — numbers count up dramatically
function metricCounter(el, { from = 0, to = 100, suffix = '%' } = {}) {
  const obj = { val: from };
  return gsap.to(obj, {
    val: to,
    duration: 1.5,
    ease: "power2.out",
    onUpdate: () => {
      el.textContent = Math.round(obj.val) + suffix;
    }
  });
}

// 5. GRAVITY DROP — text falls from above with bounce
function gravityDrop(el, { bounce = 0.3 } = {}) {
  return gsap.from(el, {
    y: -200,
    duration: 0.8,
    ease: `bounce.out`,
  });
}
```

### Text Exit Animations

```javascript
// 1. DISSOLVE UP — fade out while drifting up
function dissolveUp(el) {
  return gsap.to(el, {
    y: -30,
    opacity: 0,
    duration: 0.5,
    ease: "power2.in",
  });
}

// 2. SCALE PUNCH OUT — scale up and vanish
function scalePunchOut(el) {
  return gsap.to(el, {
    scale: 1.3,
    opacity: 0,
    duration: 0.3,
    ease: "power3.in",
  });
}

// 3. SPLIT APART — words scatter in opposite directions
function splitApart(el) {
  const words = el.querySelectorAll('.cf-word');
  const tl = gsap.timeline();
  words.forEach((w, i) => {
    const dir = i % 2 === 0 ? -1 : 1;
    tl.to(w, { x: dir * 200, opacity: 0, duration: 0.4, ease: "power3.in" }, 0);
  });
  return tl;
}
```

---

## Component Library

### Phone Mockup

```html
<!-- CinemaForge Phone Mockup -->
<div class="cf-phone" style="
  width: 280px;
  height: 580px;
  background: #1a1a1a;
  border-radius: 40px;
  border: 3px solid #333;
  padding: 12px;
  box-shadow: 
    0 25px 60px rgba(0,0,0,0.5),
    0 0 0 1px rgba(255,255,255,0.05),
    inset 0 0 0 1px rgba(255,255,255,0.03);
  position: relative;
  overflow: hidden;
">
  <!-- Notch -->
  <div style="
    width: 120px; height: 28px;
    background: #000;
    border-radius: 0 0 20px 20px;
    position: absolute;
    top: 0; left: 50%;
    transform: translateX(-50%);
    z-index: 10;
  "></div>
  
  <!-- Screen Content -->
  <div class="cf-phone-screen" style="
    width: 100%; height: 100%;
    background: #0a0a0a;
    border-radius: 28px;
    overflow: hidden;
  ">
    <!-- App UI goes here -->
  </div>
</div>
```

### Browser Window

```html
<!-- CinemaForge Browser Window -->
<div class="cf-browser" style="
  width: 800px;
  background: #1a1a1a;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 30px 80px rgba(0,0,0,0.6);
  border: 1px solid rgba(255,255,255,0.08);
">
  <!-- Chrome bar -->
  <div style="
    height: 40px;
    background: #262626;
    display: flex;
    align-items: center;
    padding: 0 16px;
    gap: 8px;
  ">
    <div style="width:12px;height:12px;border-radius:50%;background:#ff5f57"></div>
    <div style="width:12px;height:12px;border-radius:50%;background:#febc2e"></div>
    <div style="width:12px;height:12px;border-radius:50%;background:#28c840"></div>
    <div style="
      flex: 1;
      height: 24px;
      background: #1a1a1a;
      border-radius: 6px;
      margin-left: 12px;
      display: flex;
      align-items: center;
      padding: 0 12px;
    ">
      <span style="color:#666;font-size:12px;font-family:'Geist Mono',monospace">
        app.example.com
      </span>
    </div>
  </div>
  
  <!-- Page Content -->
  <div class="cf-browser-content" style="
    min-height: 450px;
    background: #0a0a0a;
    padding: 24px;
  ">
    <!-- Dashboard / UI goes here -->
  </div>
</div>
```

### Dashboard Card

```html
<!-- CinemaForge Metric Card -->
<div class="cf-card" style="
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 16px;
  padding: 24px;
  backdrop-filter: blur(20px);
">
  <div style="
    color: rgba(255,255,255,0.4);
    font-size: 13px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 8px;
  ">Monthly Revenue</div>
  
  <div style="
    color: #fff;
    font-size: 48px;
    font-weight: 700;
    letter-spacing: -0.02em;
    line-height: 1;
  ">$2.4M</div>
  
  <div style="
    color: #34d399;
    font-size: 14px;
    font-weight: 500;
    margin-top: 8px;
    display: flex;
    align-items: center;
    gap: 4px;
  ">↑ 23.5%</div>
</div>
```

### Feature Callout Line

```html
<!-- CinemaForge Callout Line -->
<svg class="cf-callout" width="200" height="2" style="overflow:visible">
  <line x1="0" y1="1" x2="200" y2="1" 
    stroke="rgba(255,255,255,0.2)" 
    stroke-width="1"
    stroke-dasharray="200"
    stroke-dashoffset="200"
    class="cf-callout-line" />
  <circle cx="0" cy="1" r="4" fill="#43d3c9" class="cf-callout-dot" opacity="0" />
</svg>

<script>
// Animate the callout drawing itself
gsap.timeline()
  .to('.cf-callout-line', { strokeDashoffset: 0, duration: 0.6, ease: "power2.out" })
  .to('.cf-callout-dot', { opacity: 1, scale: 1, duration: 0.3, ease: "back.out(2)" }, 0.4);
</script>
```

---

## Color System

### Dark Mode First (The CinemaForge Default)

```javascript
const CF_PALETTES = {
  // DEFAULT — Deep space dark
  midnight: {
    bg:      '#070708',
    surface: '#111113',
    card:    'rgba(255,255,255,0.03)',
    border:  'rgba(255,255,255,0.06)',
    fg:      '#f2f2f2',
    muted:   'rgba(255,255,255,0.4)',
    accent:  '#43d3c9',  // Teal
  },
  
  // ELECTRIC — High energy tech
  electric: {
    bg:      '#0a0a0f',
    surface: '#12121a',
    card:    'rgba(99,102,241,0.08)',
    border:  'rgba(99,102,241,0.15)',
    fg:      '#ffffff',
    muted:   'rgba(255,255,255,0.5)',
    accent:  '#6366f1',  // Indigo
  },
  
  // EMBER — Warm premium
  ember: {
    bg:      '#0c0a08',
    surface: '#161210',
    card:    'rgba(251,146,60,0.06)',
    border:  'rgba(251,146,60,0.12)',
    fg:      '#fafaf9',
    muted:   'rgba(255,255,255,0.45)',
    accent:  '#fb923c',  // Orange
  },
  
  // ARCTIC — Clean minimal
  arctic: {
    bg:      '#fafafa',
    surface: '#ffffff',
    card:    'rgba(0,0,0,0.02)',
    border:  'rgba(0,0,0,0.06)',
    fg:      '#0a0a0a',
    muted:   'rgba(0,0,0,0.4)',
    accent:  '#0ea5e9',  // Sky blue
  },
  
  // NEON — Cyberpunk edge
  neon: {
    bg:      '#050505',
    surface: '#0a0a0a',
    card:    'rgba(168,85,247,0.06)',
    border:  'rgba(168,85,247,0.15)',
    fg:      '#ffffff',
    muted:   'rgba(255,255,255,0.5)',
    accent:  '#a855f7',  // Purple
  },
};
```

### Texture & Light

```css
/* CinemaForge film grain overlay */
.cf-grain::after {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 9999;
  opacity: 0.5;
  mix-blend-mode: overlay;
}

/* CinemaForge ambient glow */
.cf-glow {
  position: absolute;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  background: radial-gradient(circle, var(--accent) 0%, transparent 70%);
  opacity: 0.08;
  filter: blur(80px);
  pointer-events: none;
}

/* CinemaForge glassmorphism card */
.cf-glass {
  background: rgba(255,255,255,0.04);
  backdrop-filter: blur(24px) saturate(1.2);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 16px;
}
```

---

## Transition Library

### Scene-to-Scene Transitions

```javascript
const CF_TRANSITIONS = {
  
  // CROSSFADE — elegant overlap dissolve
  crossfade(outEl, inEl, duration = 0.8) {
    const tl = gsap.timeline();
    tl.to(outEl, { opacity: 0, duration, ease: "power2.inOut" }, 0)
      .from(inEl, { opacity: 0, duration, ease: "power2.inOut" }, 0);
    return tl;
  },
  
  // PUSH — slide out left, slide in right
  push(outEl, inEl, duration = 0.6) {
    const tl = gsap.timeline();
    tl.to(outEl, { x: '-100%', duration, ease: "power3.inOut" }, 0)
      .from(inEl, { x: '100%', duration, ease: "power3.inOut" }, 0);
    return tl;
  },
  
  // SCALE MORPH — zoom into element, resolve to new scene
  scaleMorph(outEl, inEl, duration = 1) {
    const tl = gsap.timeline();
    tl.to(outEl, { scale: 3, opacity: 0, duration, ease: "power4.in" }, 0)
      .from(inEl, { scale: 0.3, opacity: 0, duration, ease: "power4.out" }, 0.2);
    return tl;
  },
  
  // WIPE — geometric mask wipe
  wipe(outEl, inEl, direction = 'right', duration = 0.6) {
    const tl = gsap.timeline();
    const clipStart = 'inset(0 0 0 0)';
    const clipEnd = direction === 'right' 
      ? 'inset(0 0 0 100%)' 
      : 'inset(0 100% 0 0)';
    tl.to(outEl, { clipPath: clipEnd, duration, ease: "power3.inOut" }, 0)
      .from(inEl, { clipPath: clipEnd, duration, ease: "power3.inOut" }, 0.1);
    return tl;
  },
  
  // DEPTH BLUR — out of focus → sharp
  depthBlur(outEl, inEl, duration = 0.8) {
    const tl = gsap.timeline();
    tl.to(outEl, { filter: 'blur(20px)', opacity: 0, scale: 1.05, duration, ease: "power2.in" }, 0)
      .from(inEl, { filter: 'blur(20px)', opacity: 0, scale: 0.95, duration, ease: "power2.out" }, 0.2);
    return tl;
  },
  
  // GLITCH CUT — instant cut with glitch artifact
  glitchCut(outEl, inEl) {
    const tl = gsap.timeline();
    tl.to(outEl, { opacity: 0, duration: 0.05 })
      .from(inEl, { 
        x: () => gsap.utils.random(-10, 10),
        filter: 'hue-rotate(90deg) saturate(3)',
        duration: 0.08,
      })
      .to(inEl, { x: 0, filter: 'none', duration: 0.1, ease: "power2.out" });
    return tl;
  },
};
```

---

## Staggering & Orchestration

### The CinemaForge Stagger System

```javascript
/**
 * Stagger children with the CinemaForge signature timing.
 * NOT uniform spacing — uses a custom distribution for natural feel.
 */
function cfStagger(elements, animation, config = {}) {
  const { 
    baseDelay = 0.06,     // Time between first elements
    curve = 'ease-out',    // Stagger acceleration: 'linear', 'ease-out', 'ease-in'
    maxDelay = 0.4,        // Cap total stagger spread
    direction = 'forward', // 'forward', 'reverse', 'center', 'edges'
  } = config;
  
  const count = elements.length;
  const tl = gsap.timeline();
  
  elements.forEach((el, i) => {
    let normalizedIndex;
    
    switch (direction) {
      case 'reverse':
        normalizedIndex = count - 1 - i;
        break;
      case 'center':
        normalizedIndex = Math.abs(i - (count - 1) / 2);
        break;
      case 'edges':
        normalizedIndex = (count - 1) / 2 - Math.abs(i - (count - 1) / 2);
        break;
      default:
        normalizedIndex = i;
    }
    
    let delay;
    if (curve === 'ease-out') {
      // Starts fast, slows down — most natural for reveals
      delay = baseDelay * Math.sqrt(normalizedIndex);
    } else if (curve === 'ease-in') {
      // Starts slow, speeds up — builds momentum
      delay = baseDelay * normalizedIndex * normalizedIndex / count;
    } else {
      delay = baseDelay * normalizedIndex;
    }
    
    delay = Math.min(delay, maxDelay);
    tl.add(gsap.to(el, animation), delay);
  });
  
  return tl;
}
```

### Beat-Synced Timing

```javascript
/**
 * Map animation events to musical beats.
 * BPM-driven timing ensures transitions feel rhythmic.
 */
function cfBeatMap(bpm, structure) {
  const beatDuration = 60 / bpm; // seconds per beat
  const tl = gsap.timeline();
  
  structure.forEach(({ beat, action, element, animation }) => {
    const time = (beat - 1) * beatDuration;
    tl.add(action(element, animation), time);
  });
  
  return tl;
}

// Example: 120 BPM product reveal
cfBeatMap(120, [
  { beat: 1,  action: charCascade, element: '#hook-text' },
  { beat: 5,  action: wordPunch,   element: '#problem' },
  { beat: 9,  action: (el) => gsap.from(el, { scale: 0.8, opacity: 0, duration: 0.5, ease: "back.out(1.7)" }), element: '#phone-mockup' },
  { beat: 13, action: lineWipe,    element: '#feature-1' },
  { beat: 15, action: lineWipe,    element: '#feature-2' },
  { beat: 17, action: lineWipe,    element: '#feature-3' },
  { beat: 21, action: metricCounter, element: '#metric', animation: { to: 10, suffix: 'x faster' } },
  { beat: 25, action: (el) => gsap.from(el, { y: 30, opacity: 0, duration: 0.6, ease: "power3.out" }), element: '#cta' },
]);
```

---

## Video Categories & Templates

### 1. Product Launch Ad (The Flagship)

**When:** Launching a new product, app, or major feature update.

**Structure:**
1. **Hook** — Bold problem statement in kinetic type
2. **Pain** — Visual representation of the old/broken way
3. **Reveal** — Product UI swoops in with spring physics
4. **Features** — 3–5 feature callouts with staggered entries
5. **Social Proof** — Metric counter animations
6. **CTA** — Logo + tagline + action settle

**Key Motion:**
- Phone/browser mockup enters with `CF_SPRINGS.gentle` overshoot
- Feature callout lines draw themselves SVG-style
- Metrics count up with `power2.out` easing
- Background ambient glow drifts slowly

### 2. SaaS Feature Explainer

**When:** Explaining how a software feature works.

**Structure:**
1. **Context** — "You know when…" problem framing
2. **Demo** — Animated UI walkthrough inside browser mockup
3. **Highlight** — Feature spotlight with callout lines
4. **Benefit** — Metric + comparison before/after
5. **CTA** — Try it free

**Key Motion:**
- Cursor simulation inside browser window
- Click ripple effects on UI elements
- Smooth scroll simulation in mockup
- Tooltip/popover spring animations

### 3. Kinetic Typography Manifesto

**When:** Brand anthem, mission statement, or manifesto video.

**Structure:**
1. **Opening question** — Single line, massive type
2. **Building tension** — Words accelerate, cascade, punch
3. **Climax** — Full-screen word explosion
4. **Resolution** — Calm settle into brand lockup

**Key Motion:**
- Every word animated individually
- Scale changes from 200px to 48px across the arc
- Color shifts from white to accent at climax
- Beat-synced word punches

### 4. Data / Metric Showcase

**When:** Presenting statistics, growth numbers, comparisons.

**Structure:**
1. **Context number** — "Before" state
2. **Transformation** — Visual morphing/counting
3. **Result number** — "After" state with emphasis
4. **Comparison** — Side-by-side or bar chart animation

**Key Motion:**
- Counter animations with easing
- Bar/chart grows with spring physics
- Percentage rings fill with smooth easing
- Comparison slides with push transitions

### 5. Social Media Reel (9:16 Vertical)

**When:** Instagram Reels, TikTok, YouTube Shorts.

**Structure:**
1. **Instant hook** — 0.5 sec attention grab
2. **Value** — 3–5 rapid-fire points
3. **Payoff** — The "aha" moment
4. **Follow CTA** — Brand + handle

**Key Motion:**
- Vertical-first layouts
- Faster timing (0.3s transitions)
- Bolder scale changes
- Auto-looping: last frame matches first frame

### 6. UI/UX Animation Showcase

**When:** Presenting design work, interaction patterns.

**Structure:**
1. **Context** — What the app does
2. **Interaction** — Animated interaction flow
3. **Detail** — Zoom into specific micro-interactions
4. **System** — Design system components in motion

**Key Motion:**
- Realistic touch/click interactions
- Smooth page transitions
- Micro-interaction details (toggles, checkmarks)
- Design token showcase (colors, type, spacing)

---

## Render Pipeline

### HyperFrames Configuration

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { 
      background: #070708; 
      color: #f2f2f2; 
      font-family: 'Inter', system-ui, sans-serif;
      overflow: hidden;
    }
  </style>
</head>
<body>
  <div id="root" 
    data-composition-id="cinemaforge-video"
    data-start="0"
    data-duration="30"
    data-width="1920"
    data-height="1080"
    data-fps="60"
  >
    <!-- CinemaForge composition goes here -->
  </div>
  
  <script>
    const tl = gsap.timeline({ paused: true });
    
    // === CinemaForge scenes go here ===
    // Build timeline using CF_EASE, CF_SPRINGS, and component library
    
    // Register for HyperFrames renderer
    window.__timelines = window.__timelines || {};
    window.__timelines['cinemaforge-video'] = tl;
  </script>
</body>
</html>
```

### FFmpeg Export Settings

```bash
# CinemaForge 4K 60fps export with subframe motion blur
# Input: frame sequence from Playwright capture
ffmpeg -framerate 240 -i frames/%06d.png \
  -vf "tmix=frames=4:weights='1 1 1 1',fps=60" \
  -c:v libx264 -preset slow -crf 18 \
  -pix_fmt yuv420p \
  -color_primaries bt709 -color_trc bt709 -colorspace bt709 \
  -movflags +faststart \
  output.mp4

# Vertical format (9:16) for social
ffmpeg -framerate 240 -i frames/%06d.png \
  -vf "tmix=frames=4:weights='1 1 1 1',fps=60,scale=1080:1920" \
  -c:v libx264 -preset slow -crf 18 \
  -pix_fmt yuv420p \
  -movflags +faststart \
  output_vertical.mp4
```

---

## Anti-Patterns: What NEVER to Do

| Anti-Pattern | Why It's Wrong | CinemaForge Fix |
|-------------|---------------|-----------------|
| Linear motion on ANY element | Looks robotic, cheap, amateur | Always use spring or bezier easing |
| All elements enter simultaneously | Overwhelming, no hierarchy | Stagger with 2–6 frame delays |
| Uniform stagger timing | Mechanical, predictable | Use ease-out stagger curves |
| Default GSAP ease ("power1.out") | Too subtle, not distinctive | Use power3/power4 or springs |
| Hard cuts between ALL scenes | Jarring, no flow | Mix transitions: crossfade, push, morph |
| Text appearing with just opacity | Lazy, no spatial motion | Combine opacity + y/scale + easing |
| White background | Looks like a template | Dark mode first, light only when branded |
| System fonts (Arial, Helvetica) | Screams "default" | Use Inter, Geist, Satoshi, etc. |
| Oversized logos | Amateur corporate | Logo at 10–15% of frame width max |
| No film grain | Sterile digital look | Add subtle grain at 3–5% opacity |
| Ignoring safe zones | Text cut off on mobile | 10% padding from all edges |
| No motion blur | Stroboscopic, harsh | 4× subframe blending in encode |

---

## Quick Reference: CinemaForge Cheat Sheet

```
EASING:          power3.out (default) | power4.out (snappy) | back.out(1.7) (bouncy)
SPRING:          cfSpring(t, from, to, CF_SPRINGS.snappy)
DURATION:        0.3s (micro) | 0.6s (standard) | 1.0s (cinematic) | 1.5s (epic)
STAGGER:         0.03s (chars) | 0.06s (words) | 0.1s (cards) | 0.15s (sections)
OVERSHOOT:       15% for UI | 25% for playful | 5% for subtle
ANTICIPATION:    Scale 95% for 3 frames before scaling up
SETTLE:          2–3 oscillations, amplitude < 2% of travel distance
GRAIN:           fractalNoise, opacity 3–5%, overlay blend
SAFE ZONE:       10% padding all edges
FRAMERATE:       60fps output, 240fps capture for 4× motion blur
```

---

## Example: Complete 30-Second Product Launch

See [examples/product-launch.html](examples/product-launch.html) for a fully annotated HyperFrames composition demonstrating every technique in this skill.

---

## 👥 Authors & Core Contributors

CinemaForge is built and maintained with precision by:

- **[birulyy2121](https://github.com/birulyy2121)** — Creator & Architecture Lead
- **[Google Antigravity](https://github.com/google-deepmind)** — Autonomous Systems & Multi-Agent Protocol Integration
- **[Arsh118198Imad](https://github.com/Arsh118198Imad)** — Core Engine & Agent Runtime Mechanics
- **[arhamshahbaz3499-ux](https://github.com/arhamshahbaz3499-ux)** — UX Lead, Terminal Interface & Design System
- **[shahzebejazsyed-gif](https://github.com/shahzebejazsyed-gif)** — Visual Assets & Media Architecture

Inspired by the groundbreaking work of [Null Motion](https://www.nullmotion.com/).

Licensed under MIT. Free forever.
