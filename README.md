# Denia – Classified Subject File #F-7741

A themed character dossier webpage for Denia from Wuthering Waves, designed with a classified military/intelligence aesthetic.

## 🎭 Overview

This project presents Denia's character information in the style of a classified government file, complete with:
- Dark, noir-themed UI with fusion purple and cyan accents
- **Multi-layer parallax backdrop** (far / mid / near planes + pointer parallax)
- **Self-hosted media** — images ship with the repo
- Animated particle system for atmospheric effects
- Scroll-triggered reveal animations
- Responsive design for all devices
- Loading screen with glitch effects

## ✨ Features

- **Classified Dossier Theme**: Military/intelligence aesthetic with redacted text elements
- **Parallax Engine**: Three backdrop planes travelling at different speeds and directions over the whole document, per-card depth planes in the gallery, scroll drift on content blocks and eased pointer parallax — all disabled automatically under `prefers-reduced-motion`
- **Particle Animation System**: Floating dust/data particles in the background
- **Interactive Elements**: 
  - Hover effects with glitch animations
  - Smooth scroll navigation
- **Responsive Design**: Fully responsive layout using Tailwind CSS
- **Accessibility**: Reduced motion support, proper ARIA labels

## 🛠️ Tech Stack

- **HTML5**: Semantic markup
- **Tailwind CSS**: Utility-first styling (via CDN)
- **Vanilla JavaScript**: 
  - Parallax engine (scroll + pointer)
  - Particle system
  - Scroll reveal animations
  - Loading screen logic
- **Phosphor Icons**: Icon library
- **Google Fonts**: Inter and JetBrains Mono

## 📁 Project Structure

```
denia/
├── index.html            # Main HTML file (self-contained apart from CDN CSS/fonts)
└── assets/
    └── img/
    │   ├── hero-portrait.webp      # Hero subject portrait (900×1200)
    │   ├── subject-fullbody.webp   # Dossier full-body plate (900×1203)
    │   ├── capture-01…04.webp      # Surveillance gallery tiles (640×640)
    │   ├── bg-stars.webp           # Far parallax plane (1920×1080)
    │   └── bg-bubbles.webp         # Near parallax plane (1920×1080)
```

All media is committed to the repository, so the page renders identically offline and
never breaks because a third-party host goes down. Image credits belong to Kuro Games
and the original artists — this is an unofficial fan project.

## 🚀 Usage

Simply open the HTML file in any modern web browser. No build process or dependencies required.

```bash
# Open in browser
open index.html

# Or serve it locally
python3 -m http.server 8080
```

## 🪄 Parallax

One rAF loop in `index.html` drives four kinds of depth. Everything is expressed as
CSS custom properties, so the motion composes with the reveal animations and hover
transforms instead of overwriting them.

### Backdrop planes

The stage is `position: fixed`, so each plane's travel is driven by **document
progress** (0 at the top, 1 at the bottom) rather than raw scroll offset. That is what
keeps the backdrop in motion for the whole page — the previous build ran out of room
after one viewport and then sat still.

| Plane  | Source                    | Speed | Direction            | Pointer |
|--------|---------------------------|-------|----------------------|---------|
| Far    | `assets/img/bg-stars.webp`| `0.45`| drifts **down** with the page | `10px` |
| Mid    | CSS gradients (no image)  | `-0.85`| drifts **up** against it | `20px` |
| Near   | `assets/img/bg-bubbles.webp`| `-1`| drifts up, fastest    | `34px`  |

Each plane is oversized by `--px-bleed` on every side and its travel is clamped to
that same budget, so an edge can never come into view. Planes also get a subtle
`scale()` over the scroll and the front two recede toward the footer — never to zero,
so the depth survives to the end of the page.

Config attributes:

```html
<div class="parallax-layer px-near"
     data-px-speed="-1"      <!-- -1..1 fraction of the max travel; sign = direction -->
     data-px-pointer="34"    <!-- pointer-tilt amplitude in px -->
     data-px-scale="0.02"    <!-- zoom gained over the full scroll -->
     data-px-fade="0.4"      <!-- recede over the last 40% of the page -->
     data-px-opacity="0.34"> <!-- base opacity, preserved as the plane recedes -->
```

### Content blocks

Blocks opt in with two attributes:

```html
<div class="px-item" data-px-drift="-0.077" data-px-tilt="12"> … </div>
```

* `data-px-drift` — how far the block lags behind the viewport centre. Multiplied by
  the viewport height, so the same number behaves the same on any screen: `-0.077`
  is roughly ±50px of travel. More negative = reads as farther away.
* `data-px-tilt` — how far it follows the pointer, in px.

Document-space centres are measured with the offset temporarily zeroed, so a block's
offset can never feed back into its own measurement.

### Gallery depth planes

Each surveillance tile declares its own plane:

```html
<div class="px-item" data-px-drift="-0.075" data-px-depth="0.90"> … </div>
```

`data-px-depth` is the card's resting scale (`< 1` sits back, `> 1` comes forward).
The engine derives brightness, saturation and stacking order from the same number, so
deeper tiles are dimmer, desaturated and behind the front row — then lift on hover.

### Accessibility & performance

* Under `prefers-reduced-motion: reduce` every plane, drift and tilt is pinned to `0`
  and the rAF loop is cancelled outright.
* Touch devices (no hover pointer) get a gentle sway derived from scroll distance so
  the parallax still reads without a cursor.
* Layout is re-measured on resize (debounced), on `load`, on `document.fonts.ready`
  and via a `ResizeObserver` on `body`, so late images can't leave stale offsets.
* Only two properties change per frame per element (`--px-x` / `--px-y`, or
  `--px-lx` / `--px-ly`), and no transition touches them.

## 🎨 Customization

The color scheme is defined in the Tailwind config within the HTML:

```javascript
colors: {
    'void': '#050508',
    'noir': '#0D0A0F',
    'fusion': '#9B30FF',
    'silver': '#B8B8C0',
    'cyan-glitch': '#00E5FF',
    'wine': '#7B1FA2',
    'ice': '#E8E0F0',
    'redact': '#333340'
}
```

## 📝 Sections

1. **Hero Section**: Classified dossier with character portrait
2. **Dossier Section**: Background summary and character details
3. **Abilities Section**: Forte assessment with combat capabilities
4. **Gallery Section**: Surveillance image gallery (each tile on its own depth plane)
5. **CTA Section**: Recruitment call-to-action
6. **Footer**: Classification notice

## 🎮 Character Info

- **Name**: Denia
- **Designation**: F-7741
- **Affiliation**: Fractsidus (covert) / Startorch Academy (cover)
- **Class**: Congenital Resonator
- **Weapon**: Rectifier
- **Attribute**: Fusion
- **Forte**: "Flawless"

## 🌐 Live Preview

View the live version at: [https://zaichi234509.github.io/denia/]

## 📄 License

This is a fan project. All characters and assets belong to Kuro Games and Wuthering Waves. Not affiliated with the official game.

## 🤝 Contributing

This is a personal project. Feel free to fork and customize for your own character showcases!

---

**Classification**: OMEGA | EYES ONLY
**Clearance Level**: REQUIRED
