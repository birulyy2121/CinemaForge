# CinemaForge Easing Mathematical Foundations

In high-end motion design, easing curves dictate the perceived mass, gravity, and emotional character of an interface. Linear interpolation (`lerp`) is completely unnatural because physical objects in the universe cannot transition instantaneously between velocity states without experiencing infinite acceleration.

---

## 1. Cubic-Bézier Formulation

A cubic Bézier curve is parameterized by four control points:
$$P_0 = (0, 0), \quad P_1 = (x_1, y_1), \quad P_2 = (x_2, y_2), \quad P_3 = (1, 1)$$

The explicit parametric equation for $t \in [0, 1]$ is:
$$B(t) = (1-t)^3 P_0 + 3(1-t)^2 t P_1 + 3(1-t) t^2 P_2 + t^3 P_3$$

To evaluate $y(x)$ for a given normalized time $x$:
1. Solve for $t$ such that $B_x(t) - x = 0$ using Newton-Raphson iterations:
   $$t_{n+1} = t_n - \frac{B_x(t_n) - x}{B'_x(t_n)}$$
2. Substitute $t$ into $B_y(t)$ to obtain the interpolated value.

---

## 2. Standard CinemaForge Curve Library

### A. The Snap-In (`cubic-bezier(0.16, 1, 0.3, 1)`)
- **Profile:** Extreme initial velocity with a prolonged, exponential glide into the rest position.
- **Usage:** Screen entries, modal dialogs, kinetic typography impacts.
- **GSAP Equivalent:** `power4.out`

### B. The Smooth Departure (`cubic-bezier(0.55, 0, 0.1, 1)`)
- **Profile:** Deliberate, imperceptible initial movement that accelerates smoothly into a sudden exit cut.
- **Usage:** Outgoing scenes, discarded cards, menu collapses.
- **GSAP Equivalent:** `power2.inOut` or `power3.in`

### C. The Feature Punch (`cubic-bezier(0.22, 1, 0.36, 1)`)
- **Profile:** Sharp attack with zero hesitation; lands firmly at 80% mark and settles.
- **Usage:** Badge pop-ins, toggle switches, counter highlights.
- **GSAP Equivalent:** `power3.out`

### D. The Whip / Strobe Cut (`cubic-bezier(0.9, 0, 0.1, 1)`)
- **Profile:** Asymmetric S-curve holding initial position, whipping across 90% of screen space in 2 frames, settling instantly.
- **Usage:** Fast lateral scene transitions, whip pans.
- **GSAP Equivalent:** `expo.inOut`

---

## 3. Implementation in JavaScript

```javascript
/**
 * Standalone Zero-Dependency Cubic-Bézier Solver
 */
class CinemaEase {
  constructor(x1, y1, x2, y2) {
    this.x1 = x1; this.y1 = y1;
    this.x2 = x2; this.y2 = y2;
  }

  sampleCurveX(t) {
    return ((1 - 3 * this.x2 + 3 * this.x1) * t + (3 * this.x2 - 6 * this.x1)) * t * t + (3 * this.x1) * t;
  }

  sampleCurveY(t) {
    return ((1 - 3 * this.y2 + 3 * this.y1) * t + (3 * this.y2 - 6 * this.y1)) * t * t + (3 * this.y1) * t;
  }

  sampleDerivativeX(t) {
    return (3 * (1 - 3 * this.x2 + 3 * this.x1)) * t * t + (2 * (3 * this.x2 - 6 * this.x1)) * t + (3 * this.x1);
  }

  solveCurveX(x, epsilon = 1e-5) {
    let t = x;
    for (let i = 0; i < 8; i++) {
      const xEst = this.sampleCurveX(t) - x;
      if (Math.abs(xEst) < epsilon) return t;
      const dX = this.sampleDerivativeX(t);
      if (Math.abs(dX) < 1e-6) break;
      t -= xEst / dX;
    }
    return t;
  }

  ease(x) {
    if (x <= 0) return 0;
    if (x >= 1) return 1;
    return this.sampleCurveY(this.solveCurveX(x));
  }
}
```
