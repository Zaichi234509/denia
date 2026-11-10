# Denia – Classified Subject File #F-7741

A themed character dossier webpage for Denia from Wuthering Waves, designed with a classified military/intelligence aesthetic.

## 🎭 Overview

This project presents Denia's character information in the style of a classified government file, complete with:
- Dark, noir-themed UI with fusion purple and cyan accents
- **Multi-layer parallax backdrop** (far / near planes + pointer parallax)
- **Self-hosted media** — images ship with the repo
- Animated particle system for atmospheric effects
- Scroll-triggered reveal animations
- Responsive design for all devices
- Loading screen with glitch effects

## ✨ Features

- **Classified Dossier Theme**: Military/intelligence aesthetic with redacted text elements
- **Parallax Engine**: Scroll-driven depth for the backdrop planes and content blocks, plus eased pointer parallax on key cards — all disabled automatically under `prefers-reduced-motion`
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

The backdrop is a stack of two planes plus a set of content blocks, all driven by one
rAF loop in `index.html`:

| Plane | Element | Scroll speed | Pointer |
|-------|---------|--------------|---------|
| Far   | `assets/img/bg-stars.webp` | `-0.020` | `8px` |
| Near  | `assets/img/bg-bubbles.webp` | `+0.012` | `14px` |

Content blocks opt in with two attributes:

```html
<div class="px-item" data-px-drift="-0.048" data-px-tilt="12"> … </div>
```

* `data-px-drift` — how much the block lags behind the scroll (negative = farther away)
* `data-px-tilt` — how far it follows the pointer, in pixels

Both write into the `--px-x` / `--px-y` custom properties, so they compose with the
scroll-reveal transitions instead of fighting them. When
`prefers-reduced-motion: reduce` is set, every offset is pinned to `0` and the reveal animations are replaced by static styling.

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
