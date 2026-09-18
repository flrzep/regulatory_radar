# Regulatory Radar – demo

Single-file interactive radar of the standards and regulation landscape, in P3 CI (dark).
Open `index.html` in a browser – no build, no dependencies.

## What it shows

- **Two domains**, switchable: Robotics and Autonomous Driving.
- **Left / right halves**: Cybersecurity and Functional Safety.
- **Rings (outer → inner)**: Draft → Finalization → Published.
- **Dot colour**: the active domain's categories. Robotics splits
  Consumer/Service vs Industrial; Autonomous Driving has a single category,
  since that split doesn't apply to vehicle regulation. A domain with one
  category shows no filter chips.
- **Flag badge**: EU / US / International.
- Click any item (radar blip or list card) for a modal with scope, status,
  key requirements and a P3 perspective. List view is the default on mobile.

## Editing the content

Everything lives in the `DATA` object in `index.html`. Each domain declares its
own `cats` (id, label, dot colour) and its items reference one by id:

```js
ad: {
  label: "Autonomous Driving",
  cats: [ { id:"vehicle", label:"Standards & regulation", color:"#FFFFFF" } ],
  items: [ … ]
}
```

One entry per item:

```js
{
  id:"iso26262", name:"ISO 26262", full:"ISO 26262:2018 – …",
  axis:"safety",        // "cyber" (left half) | "safety" (right half)
  ring:"published",     // "draft" | "final" | "published"
  cat:"industrial",     // "consumer" | "industrial"
  region:"INT",         // "EU" | "US" | "INT"
  a:44, rr:0.96,        // angle in degrees, position within the ring band
  tagline:"…", meta:{…}, what:"…", req:[…], take:"…", links:[…]
}
```

`a` is the angle (0° = right along the baseline, 180° = left). `rr` (0–1) only
picks the position *within* the band that `ring` selects – the radius is derived
from `ring`, so a blip can never be plotted in a band that contradicts its
status. Labels are de-overlapped and clamped to the radar box automatically, so
angles only need to be roughly spread.

The dome is a true semicircle drawn in SVG – centred on the baseline, upper half
only – and `geom()` is the single source of truth for its centre and radius, so
the grid and the blips cannot disagree.

CI colours are CSS custom properties on `:root` (`--p3-blue`, `--bg`, …).

Content is illustrative for demo purposes and is not legal advice.
