# Deterministic Spring Physics Engine for Motion Video

Traditional animation libraries tie spring animations to `requestAnimationFrame` and a ticking wall clock. For programmatic video rendering (in headless Chrome via HyperFrames, Remotion, or Playwright), **wall-clock time is completely invalid**:
- If a frame takes 200ms to render on the GPU, a wall-clock spring will skip forward 12 frames, causing severe visual stutter and non-deterministic frame output.
- **CinemaForge springs are closed-form, deterministic mathematical functions of `t` (seconds).**

---

## 1. Underdamped Harmonic Oscillator Mathematics

A damped harmonic spring system is governed by the second-order differential equation:
$$m \frac{d^2x}{dt^2} + c \frac{dx}{dt} + k x = 0$$

Where:
- $m$: Mass
- $k$: Tension / Stiffness
- $c$: Friction / Damping coefficient

### Key Parameters:
1. **Undamped angular frequency:**
   $$\omega_0 = \sqrt{\frac{k}{m}}$$
2. **Damping ratio:**
   $$\zeta = \frac{c}{2\sqrt{km}}$$

### Regime Behaviors:
- **$\zeta < 1$ (Underdamped):** The system oscillates past the target value with an exponentially decaying envelope. **This produces the signature Apple / After Effects organic bounce.**
- **$\zeta = 1$ (Critically Damped):** The fastest return to equilibrium without any oscillation or overshoot.
- **$\zeta > 1$ (Overdamped):** The system settles slowly without oscillation (ideal for heavy luxury product moves).

---

## 2. Closed-Form Evaluation Equation

For an underdamped spring ($\zeta < 1$) moving from $x_0$ to $x_1$ with an amplitude $A = x_1 - x_0$:

$$\omega_d = \omega_0 \sqrt{1 - \zeta^2}$$
$$x(t) = x_1 - A \cdot e^{-\zeta \omega_0 t} \left[ \cos(\omega_d t) + \frac{\zeta \omega_0}{\omega_d} \sin(\omega_d t) \right]$$

---

## 3. Production Configuration Matrix

| Character | Tension ($k$) | Friction ($c$) | Mass ($m$) | Damping Ratio ($\zeta$) | Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Snappy** | 300 | 20 | 1.0 | 0.577 | Fast UI controls, checkmark pops, badge reveals |
| **Bouncy** | 180 | 12 | 1.0 | 0.447 | Playful app cards, emoji reactions, icon drops |
| **Gentle** | 120 | 26 | 1.0 | 1.186 | Subtle luxury reveals, elegant editorial typography |
| **Heavy** | 80 | 30 | 2.0 | 1.185 | Heavy device mockups, full desktop application windows |
| **Elastic** | 220 | 10 | 1.0 | 0.337 | Extreme shockwave overshoot, high-impact product stings |

---

## 4. Remotion Implementation Example

```tsx
import { interpolate, spring, useCurrentFrame, useVideoConfig } from 'remotion';

export const CinemaCard = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  // Deterministic spring mapped to frame index
  const scale = spring({
    frame,
    fps,
    config: {
      damping: 12,
      stiffness: 180,
      mass: 1,
    },
  });

  return (
    <div
      style={{
        transform: `scale(${scale})`,
        transformOrigin: 'center center',
      }}
    >
      {/* Content */}
    </div>
  );
};
```
