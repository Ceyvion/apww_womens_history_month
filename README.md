# Afropop Worldwide — Women's History Month

A single-file interactive artist showcase built for Afropop Worldwide's Women's History Month campaign. No frameworks, no dependencies — pure HTML, CSS, and JavaScript.

---

## What It Is

A full-screen, scroll-snapped web experience profiling 20 influential women in African and diasporic music. Users scroll through cinematic artist cards, a names roll call, and an interactive directory — clicking any artist opens a detailed bio modal.

---

## Structure

| Screen | Description |
|--------|-------------|
| **Intro** | Full-screen hero with "Women's History Month" title and editorial text |
| **Names Showcase** | Cinematic roll call — 20 names cascade in with staggered timing |
| **Directory** | Clickable index of all 20 artists with country origins |
| **Artist Cards ×6** | Full-screen profile cards (Fela Kuti, Kidjo, Makeba, N'Dour, King Sunny Ade, Burna Boy) |
| **Bio Modal** | Overlay with biography, source links, and Wikipedia image fetch |

---

## Tech Stack

- **Zero dependencies** — no npm, no bundler, no framework
- **HTML5 / CSS3 / Vanilla JS ES6+**
- Native CSS scroll snapping (`scroll-snap-type: y mandatory`)
- Intersection Observer API for scroll-triggered animations
- Wikipedia REST API for dynamic artist images
- WebP images (converted from PNG, 96% size reduction)

---

## Performance

| Before | After |
|--------|-------|
| 6 PNGs, ~37 MB | 6 WebPs, ~1.4 MB |
| All images loaded at once | Lazy-loaded 200px before viewport |
| No priority loading | Hero image preloaded via `<link rel="preload">` |

---

## Visual Features

- **Page entrance** — fade-up animation on load
- **Staggered text reveals** — each card's text cascades in on scroll (Intersection Observer)
- **Names cascade** — 20 names roll in sequentially, featured artists highlighted larger
- **Shimmer skeleton** — while background images load
- **Image fade-in** — backgrounds transition from transparent as they load
- **Subtle parallax** — background images shift slightly on scroll
- **Scroll progress bar** — thin line at top tracks position through the experience
- **Dissolve transition** — on artist click, surrounding text dissolves upward before bio opens
- **Bio modal fade** — opens/closes with opacity transition, content staggers in

---

## Files

```
apww_glassmorphic_/
├── artist_profiles.html          # Entire app (HTML + CSS + JS)
├── README.md                     # This file
├── kidjo.jpg                     # Angélique Kidjo photo
├── Gemini_Generated_Image_*.webp # AI-generated artist backgrounds (×6)
└── Gemini_Generated_Image_*.png  # Original PNG sources
```

---

## Artists

**Featured cards:** Fela Kuti · Angélique Kidjo · Miriam Makeba · Youssou N'Dour · King Sunny Ade · Burna Boy

**Directory (20):** Aida Samb · Angélique Kidjo · Cesária Évora · Dobet Gnahoré · Elida Almeida · Fairuz · Fatoumata Diawara · Miriam Makeba · Nneka · Oumou Sangaré · Rokia Koné · Rokia Traoré · Sabah · Sho Madjozi · Shungudzo · Tems · Tiwa Savage · Toshi Reagon · Umm Kulthum · Yemi Alade

---

## Running It

Open `artist_profiles.html` directly in any modern browser. No server required.
