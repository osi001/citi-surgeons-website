# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static marketing website for **Citi Surgeons Hospital** — a tertiary surgical facility in Benin City, Nigeria. No build tools, no package manager, no framework. All dependencies are loaded from CDN.

**Pages:** `index.html` (home), `about.html`, `services.html`, `team.html`, `contact.html`

## Running the site

Open any `.html` file directly in a browser, or serve with any static file server:

```bash
# Python (no install required)
python -m http.server 8000

# Node (if available)
npx serve .
```

## Tech stack

All loaded via CDN — no local installs needed:

- **Tailwind CSS** (`cdn.tailwindcss.com`) — utility classes with a custom config defined inline in each `<head>`
- **Alpine.js** (`unpkg.com/alpinejs@3.x.x`) — navbar scroll/open state (`x-data`, `x-init`, `:class`, `@click`)
- **AOS** (`unpkg.com/aos@2.3.1`) — scroll-triggered animations via `data-aos` attributes; initialized with `AOS.init({ duration: 600, once: true, offset: 60 })`
- **Google Fonts** — Plus Jakarta Sans (headings) and DM Sans (body)

## Design system

The same Tailwind config is duplicated in every page's `<head>`. Any color or font changes must be updated in all 5 files:

| Token | Value | Usage |
|---|---|---|
| `primary` | `#0D2B5E` | Dark navy — headings, buttons, borders |
| `accent` | `#2E6DA4` | Mid blue — links, highlights, icons |
| `navy` | `#060F1E` | Deepest dark — footer, stats bar |
| `tint` | `#F4F7FB` | Off-white — alternate section backgrounds |
| `muted` | `#5A6A7A` | Grey — body text |
| `font-heading` | Plus Jakarta Sans | All `h1`–`h6` |
| `font-body` | DM Sans | Body text |

## Page structure pattern

Every page follows the same structure:
1. `<head>` with identical CDN imports, Tailwind config, and shared CSS (`.hero-grid`, `.nav-blur`, `.wa-ping`, `.wa-float`)
2. Sticky navbar with Alpine.js scroll/mobile-open state
3. Page-specific hero (`bg-gradient-to-br from-[#0A1F45] via-primary to-[#1E3A5F]`) or sub-page header
4. Content sections alternating `bg-white` / `bg-tint`
5. Shared footer (`bg-navy`) with 4-column grid
6. Floating WhatsApp button (bottom-right, fixed)

## Key contact details embedded in the HTML

Changing these requires updating every occurrence across all pages:

- **WhatsApp / main:** `+234-803-216-1331` → `https://wa.me/2348032161331`
- **Emergency line:** `+234-807-427-8057`
- **Email:** `citisurgeons101@gmail.com`
- **Address:** 40B Country Home Motel Road, Ward 36A, Oredo, Benin City, Edo State
- **Website:** `www.citisurgeons.com.ng`

## Active page indicator

Each page manually highlights its own nav link with `border-b-2 border-accent text-accent` (desktop) and `border-l-2 border-accent bg-tint` (mobile). When adding or renaming pages, update all navbars.

## Assets

| File | Used for |
|---|---|
| `logo.png` | Navbar circular emblem |
| `banner.png` | Footer wordmark (brightness-0 invert for white rendering) |
| `hospital building.webp` | About snippet on homepage and about-page hero background |
| `hospital-exterior-2.jpg` | Hero slideshow (homepage) — exterior shot |
| `operating-theatre.jpg` | Hero slideshow + services facility showcase |
| `nurse-patient.jpg` | Hero slideshow + about "Step Inside" |
| `consultant-desk.jpg` | Hero slideshow |
| `eye-exam.jpg` | Services facility showcase (ophthalmology) |
| `optical-display.jpg` | Services facility showcase (on-site eyewear) |
| `patient-room.jpg` | Services + about — recovery rooms |
| `reception-lobby.jpg` | About "Step Inside" — reception |
| `breast-screening-banner.png` | Homepage community initiative section (Breasts Savers / BSHI free screening) |
| `ProfM .jpeg` | Prof. Moses I. Momoh — team & about pages (note: filename has trailing space before extension) |
| `citiS.jpeg` / `flyer.jpeg` | Legacy promotional flyer — currently unused |
| `prof momoh pic  (1).jpeg` | Duplicate of `ProfM .jpeg` — unused |

The homepage hero slideshow (Alpine.js, 6s auto-advance, fade transitions, pause on hover) cycles 4 images with badge captions: operating theatre → nurse with patient → consultant at desk → hospital exterior. Slide order and captions are defined inline in the `<section x-data>` block at the top of `index.html`.
