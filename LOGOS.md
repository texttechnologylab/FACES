# Logo assets

Remaining placeholder slots render a dashed box with the slot name. Placeholders
are deliberate and visible, so nothing ships to a reviewer by accident and no
slot ever renders broken.

## Swapping in a real logo

Institutional marks appear in `overrides/partials/funders.html`. Replace

```html
<span class="logo--placeholder">Goethe-Universität<small>logo placeholder</small></span>
```

with

```html
<img src="{{ 'assets/logos/goethe.svg' | url }}" alt="Goethe University Frankfurt">
```

and drop the file here. Project marks (Va.Si.Li-Lab, InterView) appear inline in
the deliverable pages as a `<span class="logo--placeholder">` inside
`<div class="faces-brand">`; swap them the same way. Screenshot placeholders
(the browser-client shots on the home page and the InterView page) use
`<div class="img-placeholder" markdown>...</div>` inside a `<figure markdown>`;
replace that div with a normal `![](...)` image line.

When the last placeholder is gone, the `.logo--placeholder` and
`.img-placeholder` rules in `docs/stylesheets/faces.css` can be deleted.

## Slots

| File | For | Status |
|---|---|---|
| `favicon.png` | Browser tab | **Added** |
| `faces-full.png` | Full FACES lockup (wordmark + icon + tagline) | **Added**, not yet placed anywhere on the site; the header still shows the site name as plain text. Two lines of small tagline text make it too detailed for a compact header logo; better suited to something like the README or a print piece. |
| `vasili-lab.svg` | Va.Si.Li-Lab | **Being designed** |
| `interview.svg` | InterView | Placeholder |
| `goethe.svg` | Goethe University Frankfurt | Needs official file |
| `ttlab.png` | Text Technology Lab | **Added** |
| `lifbi.png` | LIfBi | **Added** |
| `dfg.jpg` | Deutsche Forschungsgemeinschaft | **Added** |
| `spp2431.png` | SPP 2431 New Data Spaces | **Added** |
| `janus.png` | Janus WebRTC Server | **Added** |

## Spec for new marks

- **SVG**, all text converted to paths.
- Two lockups: **square/icon** (40-64 px in cards and nav; must survive as a
  32 px favicon) and **horizontal** (~180 px wide in the footer strip).
- Legible on both `#F6F3EE` (light) and `#262929` (dark). A monochrome-safe
  silhouette is the easiest way to guarantee this.
- Ideally picks up `#004A6F` / `#F0B600` so it sits inside the site palette.
