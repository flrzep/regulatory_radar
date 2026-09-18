# Regulatory Radar — demo

Single-file interactive radar of the standards and regulation landscape, in P3 CI (dark).
Open `index.html` in a browser — no build, no dependencies.

## What it shows

- **Two domains**, switchable: Robotics and Autonomous Driving.
- **Left / right halves**: Cybersecurity and Functional Safety.
- **Rings (outer → inner)**: Draft → Finalization → Published.
- **Dot colour**: Consumer/Service (orange) vs Industrial (blue).
- **Flag badge**: EU / US / International.
- Click any item (radar blip or list card) for a modal with scope, status,
  key requirements and a P3 perspective. List view is the default on mobile.

## Editing the content

Everything lives in the `DATA` object in `index.html`. One entry per item:

```js
{
  id:"iso26262", name:"ISO 26262", full:"ISO 26262:2018 — …",
  axis:"safety",        // "cyber" (left half) | "safety" (right half)
  ring:"published",     // "draft" | "final" | "published"
  cat:"industrial",     // "consumer" | "industrial"
  region:"INT",         // "EU" | "US" | "INT"
  a:44, rr:0.96,        // angle in degrees, position within the ring band
  tagline:"…", meta:{…}, what:"…", req:[…], take:"…", links:[…]
}
```

`a` is the angle (0° = right along the baseline, 180° = left). `rr` (0–1) only
picks the position *within* the band that `ring` selects — the radius is derived
from `ring`, so a blip can never be plotted in a band that contradicts its
status. Labels are de-overlapped and clamped to the radar box automatically, so
angles only need to be roughly spread.

CI colours are CSS custom properties on `:root` (`--p3-blue`, `--bg`, …).

Content is illustrative for demo purposes and is not legal advice.
