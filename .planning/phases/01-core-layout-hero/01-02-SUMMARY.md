---
plan: 01-02
phase: 01-core-layout-hero
status: complete
completed: 2026-05-22
commits:
  - cb9a2ad feat(01-02): replace hero placeholder with fullscreen bg image and gradient overlay
  - eb949a7 feat(01-02): add KYTOO heading, tagline, and smooth-scroll CTA button
key-files:
  modified:
    - index.html
---

## What Was Built

Full hero section inside `index.html`: VALORANT_Jett_Red_1_1.webp fills the viewport with a dark gradient overlay, large "KYTOO" heading in Rajdhani Bold, tagline placeholder, and a red CTA button that smooth-scrolls to the #san-pham section.

## Tasks Completed

| Task | Description | Status |
|------|-------------|--------|
| 1 | Replaced hero placeholder with: section#hero (relative min-h-screen flex items-center), absolute-positioned webp img (object-cover), gradient overlay div (bg-gradient-to-t from-kytoo-bg via-kytoo-bg/60 to-transparent), content wrapper div (relative z-10 text-center) | ✓ Done |
| 2 | Added: brand label (text-kytoo-red uppercase), h1 "KYTOO" (font-display font-extrabold text-7xl/md:text-9xl), tagline (text-kytoo-cream leading-relaxed), CTA anchor href="#san-pham" (bg-kytoo-red no rounded-*); html element has scroll-smooth | ✓ Done |

## Self-Check: PASSED

- [x] VALORANT_Jett_Red_1_1.webp referenced (grep returns 1)
- [x] bg-gradient-to-t from-kytoo-bg with via-kytoo-bg/60 present
- [x] h1 text = "KYTOO", font-display font-extrabold uppercase tracking-widest
- [x] CTA text = "Khám phá sản phẩm" (grep returns 1)
- [x] CTA href="#san-pham"
- [x] CTA has no rounded-* class (grep returns 0 matches for "rounded" in entire file)
- [x] html element has class scroll-smooth
- [x] Brand label "Merch Valorant Việt Nam" with text-kytoo-red

## Deviations

None — executed exactly per plan spec.
