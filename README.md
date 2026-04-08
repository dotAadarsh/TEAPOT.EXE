# 🫖 TEAPOT.EXE

> **Enterprise Teapot Infrastructure** — RFC 2324 Compliant · HTCPCP/1.0 Native · Zero Coffee Guarantee™

[![HTTP Status](https://img.shields.io/badge/HTTP-418%20I'm%20a%20Teapot-b84c2a?style=flat-square)](https://tools.ietf.org/html/rfc2324)
[![RFC](https://img.shields.io/badge/RFC-2324-c9a84c?style=flat-square)](https://tools.ietf.org/html/rfc2324)
[![Coffee Brewed](https://img.shields.io/badge/Coffee%20Brewed-0-1a1208?style=flat-square)](https://tools.ietf.org/html/rfc2324)
[![Dependencies](https://img.shields.io/badge/Dependencies-1%20(Three.js)-4caf7a?style=flat-square)](https://threejs.org)
[![License](https://img.shields.io/badge/License-Tea%20Commons%201.0-c9a84c?style=flat-square)](#license)

---

The world's most over-engineered implementation of RFC 2324. A complete enterprise SaaS landing page — custom 3D teapot, pricing tiers, fake testimonials, live HTCPCP terminal — for a server whose entire purpose is to refuse to brew coffee.

**[→ Live Demo](https://your-username.github.io/teapot-exe)**

<img width="1781" height="976" alt="TEAPOT.EXE Screenshot" src="https://github.com/user-attachments/assets/e9d30d7f-9be1-44a6-a7da-34a1a1742789" />

---

## What is this

On April 1, 1998, Larry Masinter published [RFC 2324](https://tools.ietf.org/html/rfc2324) — a fully specified internet standard for the **Hyper Text Coffee Pot Control Protocol (HTCPCP/1.0)**. It defined a `BREW` HTTP method, a `Content-Type: message/coffeemaker` header, and a single legendary error code:

```
418 I'm a Teapot
```

> *"Any attempt to brew coffee with a teapot should result in the error code '418 I'm a Teapot'. The resulting entity body MAY be short and stout."*

TEAPOT.EXE is the enterprise SaaS that RFC 2324 always deserved and absolutely never needed.

---

## Features

| Feature | Status |
|---------|--------|
| Returns `418 I'm a Teapot` | ✅ Always |
| Brews coffee | ✕ Never |
| Interactive 3D teapot (Three.js) | ✅ |
| Orbiting golden rings | ✅ |
| Steam particle system | ✅ |
| Drag to rotate / scroll to zoom | ✅ |
| Fake enterprise pricing ($∞/mo Samovar tier) | ✅ |
| Fake testimonials from "Arabica Roastwell" | ✅ |
| SOC 2 Teapot Certificate (framed) | ✅ Enterprise only |
| Quarterly tea ceremony | ✅ Enterprise only |
| Any practical value whatsoever | ✕ By design |

---

## Quick Start

No npm. No build step. No framework. One file.

```bash
git clone https://github.com/your-username/teapot-exe.git
cd teapot-exe
open index.html
```

Or just drag `index.html` into your browser. It works. It returns 418. That's it.

### Deploy to GitHub Pages

```bash
# 1. Fork or clone this repo
# 2. Go to Settings → Pages → Source: main branch / root
# 3. Visit https://your-username.github.io/teapot-exe
# 4. It will be short and stout
```

---

## Architecture

```
BREW /coffee HTTP/1.1
Host: pot.teapot.exe
Content-Type: message/coffeemaker
Accept-Additions: Sugar; Cream

──────────────────────────────────

HTTP/1.1 418 I'm a Teapot
X-Teapot-Type: short, stout
X-Coffee-Support: false
Retry-With: a coffee machine

This server is a teapot.
The requested entity body
is short and stout.
Please tip me over.
```

The architecture is a single `index.html`. The "distributed teapot infrastructure" is your browser tab.

---

## The 3D Teapot

The teapot is hand-assembled from Three.js geometry primitives — no external `.obj` or `.glb` model. Because if Larry Masinter wrote an entire RFC from scratch just to make a joke, the least I could do is build a teapot from scratch just to honor it.

```
THREE.SphereGeometry      → body (oblate-scaled)
THREE.CylinderGeometry    → neck, base ring, lid base
THREE.SphereGeometry      → lid dome, knob
THREE.CatmullRomCurve3    → spout path
THREE.TubeGeometry        → spout mesh (from curve)
THREE.CatmullRomCurve3    → handle path
THREE.TubeGeometry        → handle mesh (from curve)
THREE.TorusGeometry       → equator band, shoulder ring, collar, spout tip
THREE.BufferGeometry      → steam particles (120 pts)
THREE.TorusGeometry ×3    → orbiting decorative rings
THREE.SphereGeometry ×3   → orbiting glowing dots
```

### Rendering pipeline

- `ACESFilmicToneMapping` — cinematic warmth
- `PCFSoftShadowMap` — soft shadows from key light
- `MeshPhongMaterial` — ceramic body with warm specular
- Key light flicker via `Math.sin()` on `intensity` each frame
- Smooth camera: mouse drag + scroll zoom with lerp interpolation

### Particle system

```javascript
// 120 steam particles, each with:
// - random drift speed
// - lateral sine oscillation
// - auto-reset to spout tip when height threshold exceeded
// - global opacity pulse via sin(time)

for (let i = 0; i < particleCount; i++) {
  posArr[i*3+1] += pSpeed[i];
  posArr[i*3]   += Math.sin(time + i) * 0.003;
  pLife[i] += pSpeed[i] * 0.4;
  if (pLife[i] > 1) resetParticle(i);
}
```

---

## Design System

The aesthetic: **serious enterprise startup**, executed with complete sincerity, for a teapot.

```css
:root {
  --cream:        #f5f0e8;   /* page background */
  --ink:          #1a1208;   /* primary text, dark sections */
  --gold:         #c9a84c;   /* accents, rings, eyebrows */
  --rust:         #b84c2a;   /* CTAs, error states, 418 */
  --muted:        #8a7a60;   /* secondary text */
  --font-display: 'DM Serif Display'; /* headlines */
  --font-mono:    'DM Mono';          /* technical copy */
  --font-sans:    'Syne';             /* body text */
}
```

Type hierarchy: `DM Serif Display` for authority, `DM Mono` for anything that should look like infrastructure, `Syne` for body copy. The combo reads as Y Combinator-backed seriousness, which is the point.

---

## Pricing

| Plan | Price | Teapots | Notable Inclusion |
|------|-------|---------|-------------------|
| **Kettle** | $0/mo | 1 | Unlimited 418 responses |
| **Caddy** | $49/mo | Unlimited | Priority refusal SLA (99.9%) |
| **Samovar** | $∞/mo | Private cloud | Framed SOC 2 cert · Quarterly tea ceremony |

All plans include the Zero Coffee Guarantee™. No coffee will be brewed. This is non-negotiable.

---

## Testimonials

> *"We migrated our entire coffee infrastructure to TEAPOT.EXE and saved $0. We also now have no coffee. But the 418 responses are very fast."*
>
> **— Arabica Roastwell**, VP of Hot Liquids, BrewCorp

> *"Finally, an HTTP status code with its own SaaS. I showed this to Larry Masinter's Wikipedia page and I think he would have smiled."*
>
> **— Darjeeling Xu**, Senior Tea Engineer, Kettlebase Inc.

---

## Stack

| Layer | Technology | Reason |
|-------|------------|--------|
| 3D rendering | [Three.js r128](https://threejs.org) | It's the only dependency |
| Fonts | Google Fonts (DM Serif Display, DM Mono, Syne) | Free and beautiful |
| Framework | None | What would we need one for |
| Build tool | None | `open index.html` |
| Backend | Your browser tab | Scales to 1 concurrent teapot |
| Database | N/A | We store nothing. We refuse everything. |

---

## Contributing

Pull requests are welcome, especially if they:

- Add more useless features
- Make the teapot more short and stout
- Implement the full HTCPCP/1.0 spec including the `WHEN` method (for adding milk)
- Add a `PROPFIND` endpoint that returns a list of available teas
- Increase the number of coffees brewed (just kidding, this is a hardcoded 0)

Please do not open issues requesting coffee support. The answer is 418.

---

## The HTCPCP/1.0 Specification

For your reading pleasure: [RFC 2324](https://tools.ietf.org/html/rfc2324)

Key methods defined:
- `BREW` or `POST` — attempt to brew (will 418)
- `GET` — retrieve the current pot contents (tea, presumably)
- `PROPFIND` — retrieve teapot metadata
- `WHEN` — stop pouring milk (international users only)

Key headers:
- `Content-Type: message/coffeemaker`
- `Accept-Additions: Sugar; DryMilk; Cream`
- `Safe: yes` — this request is safe, unlike coffee

---

## License

**Tea Commons License 1.0**

Permission is granted to use, copy, modify, and distribute this software, provided that:

1. You do not attempt to brew coffee with it.
2. If you do attempt to brew coffee with it, you accept that the response will be `418 I'm a Teapot`.
3. You acknowledge that Larry Masinter was right.
4. You agree that RFC 2324 is the greatest April Fool's joke in internet history.

THE SOFTWARE IS PROVIDED "AS IS", SHORT AND STOUT. THE AUTHORS MAKE NO WARRANTIES REGARDING THE ABILITY OF THIS SOFTWARE TO PRODUCE COFFEE, AS THAT IS NOT A FEATURE. IT IS A TEAPOT.

---

## Acknowledgements

🫖 **Larry Masinter** — for RFC 2324, for HTCPCP/1.0, and for the `418 I'm a Teapot` status code that has survived every attempt to kill it.

☕ **The IETF** — for publishing it with a straight face.

🌐 **The HTTP community** — for keeping 418 alive when it could have been reassigned.

---

*Built for the [DEV April Fools Challenge 2026](https://dev.to/devteam/join-our-april-fools-challenge-for-a-chance-at-tea-rrific-prizes-1ofa) · Prize category: Best Ode to Larry Masinter*

*No coffee was brewed in the making of this project. The teapot is short. The teapot is stout. Please tip it over.*
