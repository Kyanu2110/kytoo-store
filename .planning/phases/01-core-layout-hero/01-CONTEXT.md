# Phase 1: Core Layout & Hero — Context

**Gathered:** 2026-05-22
**Status:** Ready for planning

<domain>
## Phase Boundary

Phase 1 delivers the visual skeleton of the landing page: fixed navbar, full-screen hero section, empty section placeholders for Phase 2, and a minimal footer. When complete, opening `index.html` in a browser shows a styled, branded KYTOO landing page with working mobile hamburger menu. No product content yet — that is Phase 2.

</domain>

<decisions>
## Implementation Decisions

### Navbar

- **D-01:** Logo/brand centered on navbar — nav links split evenly on both sides (mirrors Valorant official site layout from reference image)
- **D-02:** Nav links: "Sản phẩm" • "Bộ sưu tập" • "Về KYTOO" • "Liên hệ" — 4 items, anchor-link scroll to sections
- **D-03:** CTA button góc phải: "Mua ngay" → link Shopee shop (nền đỏ #FF4655, uppercase, no border-radius)
- **D-04:** Mobile (< 768px): hamburger icon (☰) mở slide-down drawer với full nav links — đóng khi click link hoặc click ngoài

### Hero Section

- **D-05:** Display heading: "KYTOO" rất lớn, uppercase, font Rajdhani Bold — giống cách "VALORANT" hiển thị trên reference
- **D-06:** Tagline: placeholder text — user sẽ cung cấp nội dung thực sau khi thấy layout
- **D-07:** Alignment: căn giữa (cả heading, tagline, CTA button)
- **D-08:** CTA trong hero: "Khám phá sản phẩm" — smooth scroll xuống section sản phẩm (không thoát trang)
- **D-09:** Background: `VALORANT_Jett_Red_1_1.webp` fullscreen, `object-cover`, overlay `bg-gradient-to-t from-[#0F1923] via-[#0F1923]/60 to-transparent`

### Typography / Fonts

- **D-10:** Display font (heading lớn): **Rajdhani Bold** (Google Fonts) — condensed, military feel, gần Valorant aesthetic
- **D-11:** Body font: **Inter** (Google Fonts) — sạch, dễ đọc cho nav, body text, labels
- **D-12:** Import cả hai từ Google Fonts CDN trong `<head>` — không cần npm

### Section Scaffold

- **D-13:** Phase 1 bao gồm empty section placeholders: `#san-pham`, `#bo-suu-tap`, `#ve-kytoo`, `#lien-he` — mỗi section có min-height và section heading placeholder để Phase 2 điền
- **D-14:** Footer đơn giản: nền tối `#0F1923`, copyright "© 2024 KYTOO Store. All rights reserved.", border-top `#2a3f52` — Phase 2 sẽ thêm Zalo/FB links

### Claude's Discretion

- Scroll behavior cho hamburger menu (CSS transition hay JS toggle class)
- Exact min-height cho empty section placeholders
- Scroll offset compensation cho sticky navbar (scrollMarginTop)

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Design System
- `CLAUDE.md` — Full design system: color palette, typography rules, layout patterns, button styles, spacing rhythm. REQUIRED reading — all implementation must follow this.

### Project Context
- `.planning/PROJECT.md` — Project goals, constraints, out-of-scope decisions
- `.planning/REQUIREMENTS.md` — Phase 1 requirements: HERO-01–04, TECH-01–02

### Assets
- `VALORANT_Jett_Red_1_1.webp` — Hero background image (root folder)
- `images/` — Product images (for Phase 2, but builder should know path exists)

### Design Inspiration
- `bef937a7b661a05103b38a4e57ffb195.jpg` — Reference image: Valorant fan site showing the exact aesthetic to follow. Key elements: centered logo navbar, full-screen hero with big display text, dark/red palette, angular cards, section structure.

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `images/*.jpg / .png` — 12 product images ready for Phase 2. Phase 1 doesn't use them but the path `images/` is established.
- `VALORANT_Jett_Red_1_1.webp` — Hero background, confirmed in root folder.

### Established Patterns
- **Single-file constraint**: Everything in `index.html`. No external CSS or JS files.
- **Tailwind CDN**: Use `<script src="https://cdn.tailwindcss.com"></script>` — configure custom colors via `tailwind.config` in a `<script>` tag.
- **Vanilla JS only**: No jQuery, no framework. DOM manipulation via `querySelector` / `classList`.

### Integration Points
- Section IDs (`#san-pham`, `#bo-suu-tap`, `#ve-kytoo`, `#lien-he`) must match navbar anchor hrefs exactly — Phase 2 will fill these sections.
- Tailwind custom config (colors, fonts) set in Phase 1 — Phase 2 reuses without re-declaring.

</code_context>

<specifics>
## Specific Ideas

- Reference image `bef937a7b661a05103b38a4e57ffb195.jpg` shows "VALORANT" in huge display text centered on hero — replicate this with "KYTOO" in Rajdhani Bold
- Navbar layout: exactly mirroring the reference — logo absolute center, links symmetric left/right
- CTA in hero scrolls down (not Shopee link) — keeps user on page to see products first
- Navbar CTA "Mua ngay" goes to Shopee — for users who already know what they want

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope.

</deferred>

---

*Phase: 1-Core Layout & Hero*
*Context gathered: 2026-05-22*
