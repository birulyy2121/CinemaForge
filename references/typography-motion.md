# Kinetic Typography Master Reference

Kinetic typography is the art of expressing meaning, tempo, and emotion through moving text. In motion graphics, typography is not passive text — it is an animated visual actor.

---

## 1. The Typographic Energy Hierarchy

1. **Impact Words (Display 80–140px):**
   - Reserve for 1 or 2 core words per scene (e.g., "FAST", "CRASH", "UNIFIED").
   - Animate with scale overshoot or character cascade.
2. **Structural Prose (Headline/Subhead 24–48px):**
   - Clean, left-aligned or centered phrases.
   - Animate via vertical transform displacement (`y: 40px -> 0px`) coupled with opacity.
3. **Utility & Metas (Caption/Mono 11–14px):**
   - Eyebrow badges, step counters, timestamps.
   - Animate with instantaneous clip-path wipes or simple fade-ins.

---

## 2. Five Foundational Kinetic Text Patterns

### Pattern A: The Character Cascade (Word Stagger)
Letters arrive sequentially like keystrokes or dominoes:
- **Delay between chars:** `0.02s` to `0.035s`.
- **Motion Vector:** `y: 100% -> 0%` paired with `rotateZ: 4deg -> 0deg`.
- **Masking:** Wrap parent in `overflow: hidden` to create an invisible boundary line.

### Pattern B: The Word Punch (Rhythmic Impact)
Words slam into place on musical downbeats:
- **Motion Vector:** `scale: 1.6 -> 1.0` with `back.out(2)`.
- **Duration:** 0.35s per word.
- **Color Accent:** Shift keyword from neutral `#F2F2F2` to `#FFCC00` or `#43D3C9` at the apex.

### Pattern C: The Geometric Line Wipe
Text emerges from behind a traveling vector line or razor edge:
- **Technique:** Animate `clipPath: inset(0 100% 0 0)` to `inset(0 0% 0 0)`.
- **Ease:** `power4.inOut` over 0.7s.
- **Accompanying Element:** Pair with a 1px vertical line drawing alongside the wipe boundary.

### Pattern D: The Kinetic Odometer / Counter
For metrics, ARR, percentages, or speed benchmarks:
- **Technique:** Do not jump numbers linearly. Accelerate rapidly through the early numbers and decelerate exponentially into the final significant digits.
- **Format:** Always include positive/negative sign indicators and unit suffixes (e.g., `$`, `M`, `%`, `ms`).

### Pattern E: The Strike & Replacement
Demonstrating problem-to-solution transition:
- **Technique:** Old text is crossed out with an animated SVG line, shifts to low opacity, and drops down as the new solution text slides up from below.

---

## 3. Safe Zones & Readability Rules

1. **The 3-Second Rule:** Never display more than 6 words on screen if the scene duration is under 2.5 seconds.
2. **Safe Padding:** Maintain at least `10%` margin on all 4 viewport edges for mobile social platforms (avoiding UI icons on Instagram/TikTok).
3. **Contrast Ratio:** Ensure minimum 7:1 contrast ratio against the background. Use subtle backdrop dark scrims or drop shadows (`0 20px 40px rgba(0,0,0,0.8)`) when overlaying video.
