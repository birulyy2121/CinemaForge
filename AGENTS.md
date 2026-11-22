# CinemaForge — Agent Instructions

## For AI Coding Agents

When this skill is loaded, you are expected to produce **professional-grade motion graphics** that pass the Agency Test: a viewer should not be able to tell whether a human motion designer or an AI agent created the video.

## Critical Rules

1. **Never use linear easing.** Every `gsap.to()`, `gsap.from()`, or CSS transition MUST specify a custom ease. `power3.out` is the minimum acceptable default.

2. **Never show all elements at once.** Use staggered timing with `cfStagger()` or manual delays. Elements enter sequentially with 2–6 frame gaps.

3. **Always use the four-act structure.** Every video has a Hook, Build, Reveal, and Resolve phase with appropriate pacing.

4. **Always apply film grain.** The `.cf-grain` overlay at 3–5% opacity must be present in every composition.

5. **Always respect safe zones.** 10% padding from all edges. No text or critical elements in the outer 10%.

6. **Always register timelines.** For HyperFrames: `window.__timelines['id'] = tl;` with `paused: true`.

7. **Use the component library.** Phone mockups, browser windows, and dashboard cards should use the CinemaForge templates, not improvised HTML.

8. **Dark mode first.** Unless the brand explicitly requires light mode, default to `CF_PALETTES.midnight`.

## Render Settings

- **Resolution:** 1920×1080 (16:9) or 1080×1920 (9:16 for social)
- **Frame rate:** 60fps output, 240fps capture for subframe motion blur
- **Codec:** H.264 CRF 18 with `movflags +faststart`
- **Motion blur:** `tmix=frames=4:weights='1 1 1 1'` in FFmpeg

## Quality Checklist

Before delivering any CinemaForge video:

- [ ] No linear motion on any element
- [ ] Staggered timing on all multi-element entries
- [ ] Spring physics or custom bezier on hero elements
- [ ] Film grain overlay present
- [ ] Safe zones respected
- [ ] Beat-synced or rhythmically timed transitions
- [ ] Dark mode palette applied
- [ ] Typography uses a premium font stack
- [ ] Overshoot/settle on at least one hero element
- [ ] 60fps output with motion blur
