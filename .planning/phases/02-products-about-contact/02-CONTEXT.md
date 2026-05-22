# Phase 2: Products, About & Contact — Context

**Gathered:** 2026-05-22
**Status:** Ready for planning

<domain>
## Phase Boundary

Phase 2 fills the 4 section placeholders built in Phase 1 with real content:
- `#san-pham` → 12-product grid with modal popup
- `#bo-suu-tap` → visual gallery (lookbook-style, no prices)
- `#ve-kytoo` → brand story, UVP, social proof numbers
- `#lien-he` → Zalo + Facebook contact links; footer update

When complete, opening `index.html` shows a full landing page with all content — user can see every product, read the brand story, and contact KYTOO. Shopee links remain placeholders; those are filled in Phase 3.

</domain>

<decisions>
## Implementation Decisions

### Product Grid (PROD-01, PROD-02, PROD-03)

- **D-01:** Grid layout — 4 cột desktop (`grid-cols-4`), 2 cột tablet (`md:grid-cols-2`), 1-2 cột mobile (`grid-cols-2` hoặc `grid-cols-1` tùy content width). 12 sản phẩm = 3 hàng trên desktop.
- **D-02:** Tên sản phẩm trên card — hiển thị tên đầy đủ (Shopee-style, không rút gọn). Font nhỏ hơn để vừa card.
- **D-03:** Thứ tự hiển thị — theo giá giảm dần (featured items đầu, accessories nhỏ sau).
- **D-04:** Click behavior — click toàn bộ card mở modal. KHÔNG có nút "Mua trên Shopee" riêng trên card.
- **D-05:** Modal content — ảnh lớn + tên đầy đủ + giá + mô tả ngắn (Claude draft, 1-2 câu) + nút "Mua trên Shopee" (link placeholder `#shopee-{product}` — điền thật Phase 3).
- **D-06:** Modal close — nút X góc phải + click overlay ngoài modal + phím Escape (Claude discretion — standard UX pattern).

### Product Data (12 sản phẩm — thứ tự giá giảm dần)

| # | File | Tên đầy đủ | Giá hiển thị |
|---|------|-----------|-------------|
| 1 | mysterybox.jpg | [TẶNG GIÁ ĐỠ + CARD] Hộp Skin Game Va-lô-Rần Bí Ẩn Dành Cho Game Thủ | 150.000₫ – 279.000₫ |
| 2 | keycap14phim.jpg | Bộ Keycap Valorant 14 Phím, Nhựa PBT Profile OEM Hình Agent Cute Dành Cho Game Thủ Không dây | 251.100₫ – 279.000₫ |
| 3 | keycapcustom.jpg | Keycaps Valorant 3D Hình Agent Cute Dành Cho Bàn Phím Cơ Tổng hợp Nhựa Tổng hợp | 279.000₫ |
| 4 | tactical.jpg | [ẢNH THẬT] Mô Hình Tactical Bear, Phụ Kiện Flex Va lô Rần Dễ Thương Xả Stress | 279.000₫ |
| 5 | wingman.jpg | [ẢNH THẬT] Mô Hình Wingman, Phụ Kiện Flex Va lô Rần Dễ Thương Xả Stress | 152.100₫ |
| 6 | blindbox.jpg | [MUA MÓC KHOÁ TẶNG STICKER] - Túi mù Móc khoá Valorant Skin Dành Cho Game Thủ Valorant | 67.150₫ |
| 7 | nhanclove.jpg | Bộ 3 Nhẫn Clove Tuỳ Chỉnh Được Kích Thước, Trang Sức Valorant Đeo Tay, Độc Đáo Cho Duo Của Bạn | 79.000₫ |
| 8 | nhandaychuyen.png | Nhẫn Sage Valorant, Đồ Trang Sức Valorant | 37.000₫ – 44.100₫ |
| 9 | nuochoa.jpg | Nước Hoa Va Lo Rừng Dung Tích 10ml Tăng Cá Tính Cùng Agent Của Bạn. Hương Hoa Cỏ Tự Nhiên, Lưu Hương Lâu | 69.000₫ |
| 10 | padchuot.jpg | Tấm Lót Chuột Va-Lô-Rừng HandMade Cỡ Nhỏ 30x25cm Dành Cho Game Thủ Siêu Ngầu | 63.200₫ – 79.000₫ |
| 11 | miengketay.jpg | Miếng Kê Tay Hình Thú Corgi Siêu Cute Giúp Bảo Vệ Cổ Tay Khi Sử Dụng Máy Tính | 55.200₫ |
| 12 | meotreomanhinh.jpg | Mô Hình Mèo Trang Trí Màn Hình Máy Tính Và Bàn Làm Việc Dễ Thương | 35.000₫ |

**Lưu ý naming:** tactical.jpg = Tactical Bear, wingman.jpg = Wingman (tên file bị đặt ngược — map đúng như bảng trên).

### Bộ Sưu Tập Section

- **D-07:** Section `#bo-suu-tap` là photo gallery thuần visual — không có tên/giá/button. Dùng lại 12 ảnh sản phẩm, layout CSS grid hoặc masonry bất đối xứng (per CLAUDE.md Gallery Grid pattern). Phong cách lookbook — ảnh to, fill full cell, object-cover.

### About & Contact

- **D-08:** About section (`#ve-kytoo`) — Claude draft brand description + UVP (Valorant-themed Vietnamese merch, chất lượng, thiết kế độc quyền). Social proof numbers: dùng placeholder "1.000+" đơn đã bán / "4.8★" rating — user điền số thật Phase 3.
- **D-09:** Contact section (`#lien-he`) — hiển thị icon Zalo + icon Facebook với link placeholder (`#zalo-placeholder`, `#facebook-placeholder`). User điền link thật Phase 3. Footer thêm social links cùng lúc.

### Claude's Discretion

- Modal implementation: pure Vanilla JS overlay, không dùng library
- Modal animation: CSS opacity/transform transition nhẹ (200ms)
- Card hover effect: `scale-105` + `border-kytoo-red` (per CLAUDE.md Cards pattern)
- Gallery layout: CSS grid với `grid-template-columns: repeat(auto-fill, minmax(...))`hoặc span 2 cho featured images
- About section layout: 2-column (text trái, số liệu phải) hoặc centered — tùy aesthetic
- Mô tả ngắn trong modal: 1-2 câu, Claude draft dựa theo tên sản phẩm
- Màu giá trên card: `text-kytoo-red` (per CLAUDE.md)

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Design System
- `CLAUDE.md` — Full design system (REQUIRED): color palette, card patterns (`rounded-none`, `hover:border-kytoo-red`), button patterns (no border-radius), gallery grid (masonry, `gap-1`/`gap-2`), section alternating backgrounds, spacing rhythm (`py-20` / `max-w-7xl`)

### Project Context
- `.planning/PROJECT.md` — Project goals, constraints, out-of-scope (no cart, Shopee-only, single-file)
- `.planning/REQUIREMENTS.md` — PROD-01–03, ABOUT-01–03, CONTACT-01 requirements
- `.planning/phases/01-core-layout-hero/01-CONTEXT.md` — Phase 1 decisions (fonts, tokens, section IDs, footer)

### Phase 1 Output (read before modifying index.html)
- `.planning/phases/01-core-layout-hero/01-01-SUMMARY.md` — HTML skeleton: Tailwind config, navbar, section IDs, footer structure
- `.planning/phases/01-core-layout-hero/01-02-SUMMARY.md` — Hero section: custom tokens usable without re-declaration

### Assets
- `images/` — 12 product images (filenames listed in D-07 product data table above)
- `index.html` — Single-file to modify; ALL changes go here

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- Tailwind custom tokens (`kytoo-*`) declared in `index.html` `<script>` — reuse without re-declaring: `bg-kytoo-bg`, `bg-kytoo-bg-alt`, `text-kytoo-red`, `border-kytoo-border`, `font-display` (Rajdhani), `font-body` (Inter), `scroll-mt-navbar`
- Section placeholders `#san-pham`, `#bo-suu-tap`, `#ve-kytoo`, `#lien-he` already exist with correct background alternation (bg-kytoo-bg / bg-kytoo-bg-alt)
- JS script block at bottom of body — add modal + gallery JS here, don't create new `<script>` tags

### Established Patterns
- **No `rounded-*` anywhere** — strict per CLAUDE.md; cards, buttons, modal container all angular
- **Section headings** — `<div class="flex items-center gap-2 mb-4"><span class="w-8 h-0.5 bg-kytoo-red"></span><h2 class="font-display font-bold uppercase tracking-widest">...</h2></div>` — reuse exact pattern from existing placeholders
- **Button/CTA** — `bg-kytoo-red text-white uppercase tracking-widest px-8 py-3 hover:bg-kytoo-red-dark transition-colors` — no `rounded-*`
- **Section padding** — `py-20` desktop, `max-w-7xl mx-auto px-4` container

### Integration Points
- Replace `<p class="text-kytoo-gray text-sm">— Phase 2 content —</p>` inside each section with real content
- Modal element: add as last child of `<body>` before closing `</body>`, hidden by default (`hidden` class)
- Footer `<footer>` already exists — add Zalo/FB social links inside existing footer structure

</code_context>

<specifics>
## Specific Ideas

- Product data is complete (12 items) — use EXACTLY the names from the D-07 table, prices verbatim
- tactical.jpg naming: the file is named "tactical" but shows Tactical Bear character; wingman.jpg shows Wingman — use names from product data table, not assumptions from filename
- Price ranges: displayed as "150.000₫ – 279.000₫" format (em dash, ₫ symbol) — consistent across all range prices
- Gallery differentiator: no text overlays on gallery images — this is what makes #bo-suu-tap visually different from #san-pham

</specifics>

<deferred>
## Deferred Ideas

- Actual Shopee product links — Phase 3 fills placeholders
- Actual Zalo + Facebook URLs — Phase 3
- Social proof real numbers (actual order count, actual rating) — Phase 3
- Badge/labels on products (Mới, Hot, Bestseller) — v2 backlog per REQUIREMENTS.md
- Google Analytics / Open Graph SEO — v2 per REQUIREMENTS.md
- Formspree contact form — v2 per REQUIREMENTS.md

</deferred>

---

*Phase: 2-Products, About & Contact*
*Context gathered: 2026-05-22*
