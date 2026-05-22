# Phase 2: Products, About & Contact — Research

**Researched:** 2026-05-22
**Domain:** Vanilla JS modal, CSS grid, Tailwind CDN, single-file HTML content sections
**Confidence:** HIGH

---

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions

- **D-01:** Grid layout — 4 cột desktop (`grid-cols-4`), 2 cột tablet (`md:grid-cols-2`), `grid-cols-2` mobile (12 sản phẩm = 3 hàng desktop).
- **D-02:** Tên sản phẩm trên card — hiển thị tên đầy đủ, font nhỏ hơn để vừa card.
- **D-03:** Thứ tự hiển thị — theo giá giảm dần (featured items đầu).
- **D-04:** Click toàn bộ card mở modal. KHÔNG có nút "Mua trên Shopee" riêng trên card.
- **D-05:** Modal — ảnh lớn + tên đầy đủ + giá + mô tả ngắn 1-2 câu + nút "Mua trên Shopee" (link `#shopee-{product}`).
- **D-06:** Modal close — nút X + click overlay + phím Escape.
- **D-07:** `#bo-suu-tap` — photo gallery thuần visual, dùng lại 12 ảnh sản phẩm, CSS grid masonry bất đối xứng, không có text overlay.
- **D-08:** About (`#ve-kytoo`) — brand description + UVP, placeholder numbers "1.000+" đơn / "4.8★" rating.
- **D-09:** Contact (`#lien-he`) — Zalo + Facebook icon/link placeholders (`#zalo-placeholder`, `#facebook-placeholder`); footer thêm social links.

### Claude's Discretion

- Modal implementation: pure Vanilla JS overlay
- Modal animation: CSS opacity/transform transition 200ms
- Card hover: `scale-105` + `border-kytoo-red`
- Gallery layout: CSS grid với `grid-template-columns: repeat(auto-fill, minmax(...))` hoặc span 2 cho featured
- About layout: 2-column (text trái, số liệu phải) hoặc centered
- Mô tả modal: 1-2 câu, Claude draft
- Giá trên card: `text-kytoo-red`

### Deferred Ideas (OUT OF SCOPE)

- Actual Shopee product links — Phase 3
- Actual Zalo + Facebook URLs — Phase 3
- Social proof real numbers — Phase 3
- Badge/labels on products (Mới, Hot, Bestseller) — v2 backlog
- Google Analytics / Open Graph SEO — v2
- Formspree contact form — v2
</user_constraints>

---

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| PROD-01 | Grid card: ảnh + tên + giá từng sản phẩm | CSS grid pattern, card HTML structure, Tailwind tokens confirmed |
| PROD-02 | Nút "Mua trên Shopee" riêng từng sản phẩm | Modal contains the CTA; card click triggers modal (D-04 decision) |
| PROD-03 | Modal/popup chi tiết khi click card | Vanilla JS modal pattern fully documented |
| ABOUT-01 | Section giới thiệu thương hiệu KYTOO.GG | Section placeholder confirmed at `#ve-kytoo` |
| ABOUT-02 | UVP rõ ràng | About section layout pattern documented |
| ABOUT-03 | Số liệu uy tín (orders, rating) | Placeholder numbers approach confirmed |
| CONTACT-01 | Icon/link Zalo và Facebook | SVG inline pattern + placeholder link approach documented |
</phase_requirements>

---

## Summary

Phase 2 fills four existing section placeholders (`#san-pham`, `#bo-suu-tap`, `#ve-kytoo`, `#lien-he`) in a single `index.html`. The HTML skeleton is already complete from Phase 1 — no new files, no build step, no npm installs. The only work is replacing the `<p class="text-kytoo-gray text-sm">— Phase 2 content —</p>` stub inside each section, adding a modal element before `</body>`, and extending the existing `<script>` block at the bottom.

The entire implementation is pure HTML + Tailwind utility classes + inline Vanilla JS. At 12 products with ~100 bytes of data per product object, inline JS data is approximately 1.2 KB — negligible for this scale, no performance concern. The Tailwind CDN serves v3.x with JIT, so arbitrary values like `grid-cols-[repeat(auto-fill,_minmax(200px,_1fr))]` work without configuration changes.

The only non-trivial implementation is the modal. The standard Vanilla JS modal pattern (overlay div + inner content div, toggled by `classList`) is well understood and does not require a library. CSS native masonry (`grid-template-rows: masonry`) is NOT production-ready in 2025/2026 for stable cross-browser use — the safe approach for gallery is CSS grid with explicit `grid-column: span 2` on featured cells, which works in all browsers today with Tailwind's `col-span-2` class.

**Primary recommendation:** Two plans — `02-01` (product grid + modal JS) and `02-02` (gallery, about, contact, footer update). All changes to `index.html` only.

---

## Project Constraints (from CLAUDE.md)

| Directive | Impact on Phase 2 |
|-----------|-------------------|
| Single-file: all code in `index.html` | No new `.js`, `.css`, or `.html` files |
| Tailwind CDN — no npm, no build step | All styling via utility classes; arbitrary values use `[...]` syntax |
| NO `rounded-*` anywhere | Cards, modal container, buttons — all angular |
| Design system colors only (`kytoo-*` tokens) | No inline hex colours outside of established tokens |
| Buttons: no border-radius, uppercase, tracking-widest | `bg-kytoo-red text-white uppercase tracking-widest px-8 py-3` |
| Cards: `rounded-none`, border `border-kytoo-border`, hover `border-kytoo-red` | Exact hover pattern: `hover:border-kytoo-red hover:scale-105` |
| Gallery: gap-1/gap-2, object-cover, no text overlay | `gap-2` between gallery cells |
| Section padding: `py-20` / `max-w-7xl mx-auto px-4` | All 4 sections already have this in place |
| JS in existing `<script>` block — no new `<script>` tags | Append modal JS and product data to existing script at bottom of `<body>` |
| Icons: Lucide CDN or SVG inline | For Zalo/Facebook: use SVG inline (no Lucide for social brand icons) |
| Mobile-first responsive testing required | Grid: `grid-cols-2` base → `md:grid-cols-2` → `lg:grid-cols-4` |

---

## Architectural Responsibility Map

| Capability | Primary Tier | Secondary Tier | Rationale |
|------------|-------------|----------------|-----------|
| Product grid rendering | Browser / Client (HTML) | — | Static data, no API; hardcoded HTML or JS-generated DOM |
| Modal open/close logic | Browser / Client (JS) | — | Pure DOM toggle, no server |
| Gallery layout | Browser / Client (CSS) | — | CSS grid span pattern |
| About/UVP copy | Browser / Client (HTML) | — | Static text |
| Contact links | Browser / Client (HTML) | — | Anchor tags, placeholder hrefs |
| Shopee link routing | Out of scope (Phase 3) | — | Placeholder `#shopee-{product}` format agreed |

---

## Standard Stack

### Core (already installed — no new packages needed)

| Library | Version | Purpose | Why Standard |
|---------|---------|---------|--------------|
| Tailwind CSS CDN | v3.x (JIT) | All utility classes | Established in Phase 1; `tailwind.config` extends are live |
| Vanilla JS | ES2020 (browser native) | Modal logic, event handling | CLAUDE.md constraint — no frameworks |
| Google Fonts (Rajdhani + Inter) | already loaded | Typography | Established in Phase 1 |

[VERIFIED: index.html line 10 — `https://cdn.tailwindcss.com`]

### No New Packages

This phase installs **zero** external packages. Everything is either already in `index.html` or implemented as inline HTML/CSS/JS. The Package Legitimacy Audit section is omitted — no packages to audit.

---

## Architecture Patterns

### System Architecture Diagram

```
User opens index.html
        |
        v
[Browser renders static HTML]
        |
    +---+---+
    |       |
    v       v
[4 sections  [Modal element (hidden)]
 filled]          |
    |         [JS event listeners]
    |              |
[Card click] ------+----> [openModal(productId)]
                          - populate modal DOM
                          - remove 'hidden' class
                          - add body overflow-hidden

[Overlay click / X click / Escape] --> [closeModal()]
                                        - add 'hidden' class
                                        - remove body overflow-hidden
```

### Recommended HTML Structure

All changes are in `index.html`. The 4 placeholder sections already have the correct outer shell — only the inner content changes.

**Section replacement pattern:** Each section currently ends with:
```html
<p class="text-kytoo-gray text-sm">— Phase 2 content —</p>
```
This line is replaced with real content. The `<div class="flex items-center gap-2 mb-4">` heading row is kept as-is.

### Pattern 1: Product Card

**What:** Clickable card with image, product name, price. The entire card is a `<div>` with a click handler. No anchor tag wrapping (modal opens on click, not navigation).

**Exact structure:**
```html
<!-- Source: CLAUDE.md Cards pattern + CONTEXT.md D-04 -->
<div
  class="bg-kytoo-bg-alt border border-kytoo-border cursor-pointer transition-all duration-200 hover:border-kytoo-red hover:scale-105 group"
  onclick="openModal('mysterybox')"
>
  <div class="aspect-square overflow-hidden">
    <img src="images/mysterybox.jpg" alt="Hộp Skin Game Bí Ẩn" class="w-full h-full object-cover">
  </div>
  <div class="p-3">
    <p class="text-kytoo-cream text-xs leading-snug mb-1 line-clamp-2">[TẶNG GIÁ ĐỠ + CARD] Hộp Skin Game Va-lô-Rần Bí Ẩn Dành Cho Game Thủ</p>
    <p class="text-kytoo-red text-sm font-semibold">150.000₫ – 279.000₫</p>
  </div>
</div>
```

Key notes:
- `aspect-square` keeps all cards uniform height regardless of image dimensions [VERIFIED: Tailwind v3 docs]
- `line-clamp-2` truncates long Vietnamese product names — Tailwind CDN v3 supports this as a built-in utility [VERIFIED: Tailwind v3.3+ release notes]
- `rounded-none` is NOT needed — it is the default when no `rounded-*` class is applied
- No `<a>` wrapping: click is handled by `onclick` attribute calling a JS function

### Pattern 2: Product Grid

**What:** CSS grid container, 2 cols mobile → 2 cols tablet → 4 cols desktop.

```html
<!-- Source: CONTEXT.md D-01, CLAUDE.md card gap rhythm -->
<div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
  <!-- 12 product cards here -->
</div>
```

Note: D-01 says `md:grid-cols-2` for tablet (same as mobile). Using `lg:grid-cols-4` for the 4-col breakpoint is the cleanest Tailwind expression. `md:` is 768px, `lg:` is 1024px — 4 columns at 1024px+ gives adequate card width.

### Pattern 3: Modal

**What:** Full-screen overlay with centered card. Added as last child of `<body>` before `</body>`. Hidden by default with `hidden` class.

```html
<!-- Source: Vanilla JS modal standard pattern; CONTEXT.md D-05, D-06 -->
<div id="product-modal" class="hidden fixed inset-0 z-50 flex items-center justify-center bg-kytoo-bg/80 backdrop-blur-sm" onclick="handleModalOverlayClick(event)">
  <div class="bg-kytoo-bg-alt border border-kytoo-border w-full max-w-lg mx-4 relative" onclick="event.stopPropagation()">
    <!-- Close button -->
    <button onclick="closeModal()" class="absolute top-3 right-3 text-kytoo-gray hover:text-kytoo-cream transition-colors" aria-label="Đóng">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="square"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
    </button>
    <!-- Modal image -->
    <div class="aspect-square overflow-hidden">
      <img id="modal-img" src="" alt="" class="w-full h-full object-cover">
    </div>
    <!-- Modal content -->
    <div class="p-6">
      <p id="modal-name" class="text-kytoo-cream font-semibold text-base mb-1 leading-snug"></p>
      <p id="modal-price" class="text-kytoo-red font-bold text-lg mb-3"></p>
      <p id="modal-desc" class="text-kytoo-gray text-sm leading-relaxed mb-5"></p>
      <a id="modal-shopee-link" href="#shopee-placeholder" target="_blank" rel="noopener"
         class="block text-center bg-kytoo-red text-white uppercase tracking-widest px-8 py-3 text-sm font-semibold hover:bg-kytoo-red-dark transition-colors">
        Mua trên Shopee
      </a>
    </div>
  </div>
</div>
```

Key notes:
- Modal container is `fixed inset-0` — covers full viewport
- Inner `.max-w-lg` card uses `onClick="event.stopPropagation()"` to prevent overlay-click handler from firing when user clicks inside the card
- `handleModalOverlayClick(event)` on the outer div checks `event.target === this` before closing — or use `stopPropagation` on the inner card (both approaches work; stopPropagation is simpler)
- NO `rounded-*` on modal container or buttons — strict per CLAUDE.md
- `backdrop-blur-sm` is a Tailwind CDN v3 utility — supported [VERIFIED: Tailwind v3 docs]
- `target="_blank" rel="noopener"` on Shopee link — standard security practice

### Pattern 4: Modal JavaScript

**What:** Append to the existing `<script>` block. Use a plain JS object literal for product data — no JSON.parse, no fetch.

```javascript
// Source: Vanilla JS standard; appended to existing <script> block
const PRODUCTS = {
  mysterybox: {
    name: '[TẶNG GIÁ ĐỠ + CARD] Hộp Skin Game Va-lô-Rần Bí Ẩn Dành Cho Game Thủ',
    price: '150.000₫ – 279.000₫',
    img: 'images/mysterybox.jpg',
    desc: 'Hộp bí ẩn chứa đầy bất ngờ — mỗi hộp là một bộ skin Valorant độc đáo bạn chưa từng thấy.',
    shopee: '#shopee-mysterybox'
  },
  // ... 11 more entries
};

function openModal(productId) {
  const p = PRODUCTS[productId];
  if (!p) return;
  document.getElementById('modal-img').src = p.img;
  document.getElementById('modal-img').alt = p.name;
  document.getElementById('modal-name').textContent = p.name;
  document.getElementById('modal-price').textContent = p.price;
  document.getElementById('modal-desc').textContent = p.desc;
  document.getElementById('modal-shopee-link').href = p.shopee;
  document.getElementById('product-modal').classList.remove('hidden');
  document.body.style.overflow = 'hidden';
}

function closeModal() {
  document.getElementById('product-modal').classList.add('hidden');
  document.body.style.overflow = '';
}

function handleModalOverlayClick(event) {
  if (event.target === document.getElementById('product-modal')) {
    closeModal();
  }
}

document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') closeModal();
});
```

Data size: 12 product objects × ~150 bytes average = ~1.8 KB inline. No performance concern for a single-file landing page. [ASSUMED — estimate based on typical JS object literal sizes; no measurable impact at this scale]

### Pattern 5: Gallery Grid (CSS only)

**What:** `#bo-suu-tap` — 12 images in a bespoke grid. Two "featured" cells span 2 columns. No text overlays, no hover labels.

```html
<!-- Source: CLAUDE.md Gallery Grid pattern -->
<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-2">
  <!-- Featured (col-span-2) -->
  <div class="col-span-2 aspect-video overflow-hidden">
    <img src="images/mysterybox.jpg" alt="" class="w-full h-full object-cover" aria-hidden="true">
  </div>
  <!-- Regular cells -->
  <div class="aspect-square overflow-hidden">
    <img src="images/blindbox.jpg" alt="" class="w-full h-full object-cover" aria-hidden="true">
  </div>
  <!-- ... remaining 10 cells -->
</div>
```

Key notes:
- `col-span-2` works across all browsers — this is the CSS grid-column span approach, NOT native masonry [VERIFIED: Tailwind v3 docs; caniuse.com]
- `aspect-video` (16:9) for featured cells; `aspect-square` for regular cells — consistent heights per row
- Gallery images have `aria-hidden="true"` — they are purely decorative (lookbook style, no text)
- Native CSS masonry (`grid-template-rows: masonry`) is NOT used — it is behind flags in all browsers and NOT production-ready [VERIFIED: MDN; caniuse.com masonry search results 2025]
- Do NOT use `columns-*` (CSS multi-column) — that approach breaks insertion order and is awkward for equal-gap layout

### Pattern 6: About Section Layout

**What:** 2-column layout — brand copy left, social proof numbers right.

```html
<div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
  <!-- Left: copy -->
  <div>
    <p class="text-kytoo-cream leading-relaxed mb-4">
      KYTOO là thương hiệu merch Valorant hàng đầu Việt Nam...
    </p>
    <p class="text-kytoo-cream leading-relaxed">
      Mỗi sản phẩm được thiết kế bởi fan, dành cho fan...
    </p>
  </div>
  <!-- Right: stats -->
  <div class="flex flex-col gap-6 md:items-end">
    <div>
      <p class="text-kytoo-red font-display font-bold text-5xl tracking-widest">1.000+</p>
      <p class="text-kytoo-gray text-sm uppercase tracking-widest mt-1">Đơn đã giao</p>
    </div>
    <div>
      <p class="text-kytoo-red font-display font-bold text-5xl tracking-widest">4.8★</p>
      <p class="text-kytoo-gray text-sm uppercase tracking-widest mt-1">Đánh giá trên Shopee</p>
    </div>
  </div>
</div>
```

### Pattern 7: Contact Section + Footer Update

**What:** Zalo + Facebook links with SVG icons. Also update footer to add same links.

```html
<!-- Contact cards (inside #lien-he section, after heading) -->
<div class="flex flex-col sm:flex-row gap-4">
  <a href="#zalo-placeholder" class="flex items-center gap-3 border border-kytoo-border bg-kytoo-bg-alt px-6 py-4 hover:border-kytoo-red transition-colors group">
    <!-- Zalo SVG icon inline -->
    <svg ...><!-- Zalo 'Z' icon --></svg>
    <div>
      <p class="text-kytoo-cream font-semibold text-sm uppercase tracking-widest">Zalo</p>
      <p class="text-kytoo-gray text-xs">Nhắn tin trực tiếp</p>
    </div>
  </a>
  <a href="#facebook-placeholder" class="flex items-center gap-3 border border-kytoo-border bg-kytoo-bg-alt px-6 py-4 hover:border-kytoo-red transition-colors group">
    <!-- Facebook SVG icon inline -->
    <svg ...><!-- Facebook 'f' icon --></svg>
    <div>
      <p class="text-kytoo-cream font-semibold text-sm uppercase tracking-widest">Facebook</p>
      <p class="text-kytoo-gray text-xs">Like trang KYTOO</p>
    </div>
  </a>
</div>
```

Footer update — replace existing `<footer>` content:
```html
<!-- Existing footer: <p class="text-kytoo-gray text-sm">© 2024 KYTOO Store. All rights reserved.</p> -->
<!-- Replace with: -->
<div class="flex flex-col items-center gap-4">
  <div class="flex items-center gap-6">
    <a href="#zalo-placeholder" class="text-kytoo-gray hover:text-kytoo-cream transition-colors" aria-label="Zalo"><!-- SVG --></a>
    <a href="#facebook-placeholder" class="text-kytoo-gray hover:text-kytoo-cream transition-colors" aria-label="Facebook"><!-- SVG --></a>
  </div>
  <p class="text-kytoo-gray text-sm">© 2025 KYTOO Store. All rights reserved.</p>
</div>
```

Note: footer currently says "© 2024" — should update to 2025.

### Anti-Patterns to Avoid

- **`rounded-*` classes anywhere** — forbidden by CLAUDE.md; modal card, cards, buttons must all be sharp-cornered
- **Wrapping product cards in `<a>` tags** — use `<div onclick="...">` instead; wrapping in anchor adds nested interactive element confusion and makes the modal-opening pattern more complex
- **CSS `columns-*` for gallery masonry** — columns are document-flow-based and produce top-to-bottom column order, not row order; CSS grid `col-span-2` is correct
- **`grid-template-rows: masonry`** — behind browser flags, NOT production-ready
- **New `<script>` tags** — CLAUDE.md rule: add all JS to the existing `<script>` block at bottom of body
- **Inline `style=` attributes for colors** — use Tailwind tokens; no `style="color: #FF4655"`
- **`localStorage` or external API calls** — no dynamic data; all content is static inline HTML/JS

---

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Modal open/close animation | Custom CSS `@keyframes` animation | CSS `transition` on `opacity` + `transform` via Tailwind `transition-opacity duration-200` toggled by class swap | Simpler, consistent, no keyframe declaration needed |
| Product image aspect ratio enforcement | Fixed `height` in px | `aspect-square` Tailwind utility | Responsive — adapts to any card width |
| Scroll lock when modal open | Complex CSS body scroll lock | `document.body.style.overflow = 'hidden'` / `= ''` | Sufficient for single-page landing; no iframe or other scroll context |
| Gallery masonry layout | Native CSS masonry or JS library | CSS grid `col-span-2` on featured cells | Cross-browser, zero JS, zero dependency |
| Social icons | Lucide CDN (Lucide has no Zalo/Facebook brand icons) | SVG inline — simple paths only | Brand icons are not in Lucide; inline SVG is the correct pattern per CLAUDE.md |
| Product name truncation | JS substring + ellipsis | Tailwind `line-clamp-2` | Built into Tailwind CDN v3.3+; no JS required |

---

## Complete Product Data Table

All 12 items sorted by price descending (D-03). Use EXACTLY these names and prices — verbatim from CONTEXT.md.

| Key | File | Tên đầy đủ | Giá | Modal description (Claude draft) |
|-----|------|-----------|-----|----------------------------------|
| `mysterybox` | mysterybox.jpg | [TẶNG GIÁ ĐỠ + CARD] Hộp Skin Game Va-lô-Rần Bí Ẩn Dành Cho Game Thủ | 150.000₫ – 279.000₫ | Mở hộp bí ẩn để nhận bộ skin Valorant ngẫu nhiên — thêm phụ kiện giá đỡ và card đặc biệt tặng kèm. |
| `keycapcustom` | keycapcustom.jpg | Keycaps Valorant 3D Hình Agent Cute Dành Cho Bàn Phím Cơ Tổng hợp Nhựa Tổng hợp | 279.000₫ | Keycap 3D in hình Agent Valorant nổi bật, chất liệu nhựa tổng hợp bền — nâng cấp bàn phím cơ của bạn ngay. |
| `keycap14phim` | keycap14phim.jpg | Bộ Keycap Valorant 14 Phím, Nhựa PBT Profile OEM Hình Agent Cute Dành Cho Game Thủ Không dây | 251.100₫ – 279.000₫ | Bộ 14 keycap PBT chuẩn OEM in hình Agent dễ thương — tương thích với hầu hết bàn phím cơ và không dây. |
| `tactical` | tactical.jpg | [ẢNH THẬT] Mô Hình Tactical Bear, Phụ Kiện Flex Va lô Rần Dễ Thương Xả Stress | 279.000₫ | Mô hình Tactical Bear chính xác từng chi tiết — flex bàn gaming, xả stress cực hiệu quả. |
| `wingman` | wingman.jpg | [ẢNH THẬT] Mô Hình Wingman, Phụ Kiện Flex Va lô Rần Dễ Thương Xả Stress | 152.100₫ | Người bạn đồng hành Wingman thu nhỏ — trang trí bàn làm việc và flex với đồng đội cùng chung server. |
| `nhanclove` | nhanclove.jpg | Bộ 3 Nhẫn Clove Tuỳ Chỉnh Được Kích Thước, Trang Sức Valorant Đeo Tay, Độc Đáo Cho Duo Của Bạn | 79.000₫ | Bộ 3 nhẫn lấy cảm hứng từ Agent Clove — size tùy chỉnh, lý tưởng cho cặp đôi game thủ. |
| `nuochoa` | nuochoa.jpg | Nước Hoa Va Lo Rừng Dung Tích 10ml Tăng Cá Tính Cùng Agent Của Bạn. Hương Hoa Cỏ Tự Nhiên, Lưu Hương Lâu | 69.000₫ | Nước hoa mini 10ml hương thiên nhiên — mang cá tính Agent Valorant vào cuộc sống thực của bạn. |
| `blindbox` | blindbox.jpg | [MUA MÓC KHOÁ TẶNG STICKER] - Túi mù Móc khoá Valorant Skin Dành Cho Game Thủ Valorant | 67.150₫ | Móc khoá skin Valorant bí ẩn — mỗi túi mù là một skin ngẫu nhiên, kèm sticker tặng kèm. |
| `padchuot` | padchuot.jpg | Tấm Lót Chuột Va-Lô-Rừng HandMade Cỡ Nhỏ 30x25cm Dành Cho Game Thủ Siêu Ngầu | 63.200₫ – 79.000₫ | Pad chuột handmade 30×25cm in hoa văn Valorant — bảo vệ mặt bàn và tăng độ chính xác khi aim. |
| `miengketay` | miengketay.jpg | Miếng Kê Tay Hình Thú Corgi Siêu Cute Giúp Bảo Vệ Cổ Tay Khi Sử Dụng Máy Tính | 55.200₫ | Kê tay hình Corgi dễ thương — giảm mỏi cổ tay sau những session gaming dài. |
| `nhandaychuyen` | nhandaychuyen.png | Nhẫn Sage Valorant, Đồ Trang Sức Valorant | 37.000₫ – 44.100₫ | Nhẫn lấy cảm hứng từ Agent Sage — đơn giản, tinh tế, dành cho người yêu Valorant. |
| `meotreomanhinh` | meotreomanhinh.jpg | Mô Hình Mèo Trang Trí Màn Hình Máy Tính Và Bàn Làm Việc Dễ Thương | 35.000₫ | Mèo nhỏ treo mép màn hình — trang trí bàn làm việc thêm cute mà không tốn không gian. |

**File naming note:** `tactical.jpg` = Tactical Bear; `wingman.jpg` = Wingman. The filenames appear swapped in intuition but the product data table above is the authoritative mapping per CONTEXT.md. [VERIFIED: CONTEXT.md explicit note "tactical.jpg = Tactical Bear, wingman.jpg = Wingman"]

**Image format note:** `nhandaychuyen.png` is a PNG, not JPG. All other assets are `.jpg`. The `<img src>` path must use `.png` for this product. [VERIFIED: `images/` directory listing]

---

## Common Pitfalls

### Pitfall 1: rounded-* Classes Sneaking In
**What goes wrong:** Editor autocomplete suggests `rounded-lg` for the modal card or product cards; modal looks acceptable but violates the design system.
**Why it happens:** Default mental model for modals and cards includes border-radius.
**How to avoid:** After writing any card, button, or modal HTML — grep for `rounded` before considering it done. Zero matches expected.
**Warning signs:** Any `rounded-*` in the output file.

### Pitfall 2: Modal Overlay Click Fires When Clicking Inside Modal
**What goes wrong:** User clicks the Shopee button inside the modal; modal closes.
**Why it happens:** Click event bubbles from inner elements up to the overlay div that has the close handler.
**How to avoid:** Add `onclick="event.stopPropagation()"` on the inner modal card `<div>`. The overlay's `handleModalOverlayClick` must check `event.target === event.currentTarget` OR rely on stopPropagation on the inner card.
**Warning signs:** Modal closes when clicking anywhere inside it, not just the overlay.

### Pitfall 3: body overflow-hidden Not Cleared on Page Scroll
**What goes wrong:** User opens modal, closes it via Escape or X, but page is still un-scrollable.
**Why it happens:** `document.body.style.overflow = 'hidden'` set on open but not cleared in one of the three close paths (X button, overlay click, Escape key).
**How to avoid:** All three close paths must call the same `closeModal()` function which always resets `document.body.style.overflow = ''`.
**Warning signs:** Page locked after modal closes.

### Pitfall 4: img src Path for .png Product
**What goes wrong:** `images/nhandaychuyen.jpg` 404s — the file is `.png`.
**Why it happens:** All other 11 products are `.jpg`; easy to copy-paste and miss the extension.
**How to avoid:** The product data object for `nhandaychuyen` must have `img: 'images/nhandaychuyen.png'`.
**Warning signs:** One product shows broken image in grid and modal.

### Pitfall 5: line-clamp-2 Availability
**What goes wrong:** `line-clamp-2` has no effect — product names overflow cards.
**Why it happens:** `line-clamp-*` was added as a core utility in Tailwind v3.3. The CDN `cdn.tailwindcss.com` serves v3.x (confirmed). However, if an older pinned version is somehow loaded, it falls back to plugin behavior.
**How to avoid:** The CDN URL in `index.html` is `https://cdn.tailwindcss.com` (unpinned), which serves the latest v3.x. `line-clamp-2` works. No action needed.
**Warning signs:** Product names bleed outside card boundaries.

### Pitfall 6: CSS Native Masonry Used in Gallery
**What goes wrong:** Gallery layout breaks in Chrome or Firefox stable because `grid-template-rows: masonry` is not supported without a flag.
**Why it happens:** The MDN page for masonry exists and is convincing, but the feature is NOT production-ready in stable browsers as of 2025/2026.
**How to avoid:** Use CSS grid `col-span-2` on featured images. This is the plan.
**Warning signs:** Gallery cells stack incorrectly or the layout collapses in non-flag Chrome.

### Pitfall 7: Year in Footer Still Says 2024
**What goes wrong:** Footer shows "© 2024" — cosmetically wrong.
**Why it happens:** The footer was written in Phase 1 with year hardcoded as 2024. Phase 2 footer update should fix this to 2025.
**Warning signs:** "2024" visible in footer after Phase 2 execution.

---

## Environment Availability

| Dependency | Required By | Available | Version | Fallback |
|------------|------------|-----------|---------|----------|
| All 12 product images | Product grid, gallery | ✓ | N/A (files confirmed) | — |
| Tailwind CDN | All styling | ✓ | cdn.tailwindcss.com (v3.x) | — |
| Google Fonts (Rajdhani, Inter) | Typography | ✓ | Already in `<head>` | System sans-serif |
| Browser (to view result) | Testing | ✓ | Any modern browser | — |

All 12 image files confirmed present: mysterybox.jpg, blindbox.jpg, keycap14phim.jpg, keycapcustom.jpg, padchuot.jpg, nhanclove.jpg, nhandaychuyen.png, wingman.jpg, tactical.jpg, nuochoa.jpg, miengketay.jpg, meotreomanhinh.jpg.
[VERIFIED: `images/` directory listing via PowerShell]

**Missing dependencies with no fallback:** None — all dependencies available.

---

## Existing Code: Exact Integration Points

The following is the complete state of the 4 placeholder sections in `index.html` (verified by direct read):

**`#san-pham` (line 90–98):**
```html
<section id="san-pham" class="py-20 bg-kytoo-bg scroll-mt-navbar">
  <div class="max-w-7xl mx-auto px-4">
    <div class="flex items-center gap-2 mb-4">
      <span class="w-8 h-0.5 bg-kytoo-red inline-block"></span>
      <h2 class="text-3xl font-display font-bold uppercase tracking-widest text-kytoo-cream">Sản Phẩm</h2>
    </div>
    <p class="text-kytoo-gray text-sm">— Phase 2 content —</p>  <!-- REPLACE THIS LINE -->
  </div>
</section>
```

**`#bo-suu-tap` (line 100–108):**
```html
<section id="bo-suu-tap" class="py-20 bg-kytoo-bg-alt scroll-mt-navbar">
  <div class="max-w-7xl mx-auto px-4">
    <div class="flex items-center gap-2 mb-4">
      <span class="w-8 h-0.5 bg-kytoo-red inline-block"></span>
      <h2 class="text-3xl font-display font-bold uppercase tracking-widest text-kytoo-cream">Bộ Sưu Tập</h2>
    </div>
    <p class="text-kytoo-gray text-sm">— Phase 2 content —</p>  <!-- REPLACE THIS LINE -->
  </div>
</section>
```

**`#ve-kytoo` (line 110–118):**
```html
<section id="ve-kytoo" class="py-20 bg-kytoo-bg scroll-mt-navbar">
  ...same structure...
  <p class="text-kytoo-gray text-sm">— Phase 2 content —</p>  <!-- REPLACE THIS LINE -->
```

**`#lien-he` (line 120–128):**
```html
<section id="lien-he" class="py-20 bg-kytoo-bg-alt scroll-mt-navbar">
  ...same structure...
  <p class="text-kytoo-gray text-sm">— Phase 2 content —</p>  <!-- REPLACE THIS LINE -->
```

**Footer (line 131–135):**
```html
<footer class="bg-kytoo-bg border-t border-kytoo-border py-8">
  <div class="max-w-7xl mx-auto px-4 text-center">
    <p class="text-kytoo-gray text-sm">© 2024 KYTOO Store. All rights reserved.</p>  <!-- UPDATE + ADD SOCIAL LINKS -->
  </div>
</footer>
```

**Existing `<script>` block (line 137–157):** Hamburger JS already there. Modal JS and product data object are APPENDED inside this same `<script>` tag — no new `<script>` tag.

**Modal element:** Added immediately before `</body>` (after the `</script>` tag at line 157).

---

## Assumptions Log

| # | Claim | Section | Risk if Wrong |
|---|-------|---------|---------------|
| A1 | `line-clamp-2` works with current CDN v3.x | Pattern 1 (Card) | Product names overflow cards; add `overflow-hidden text-ellipsis` fallback |
| A2 | Inline JS data object ~1.8 KB is negligible | Modal JS Pattern | None practical — even 10x this size is irrelevant for a local HTML file |
| A3 | `backdrop-blur-sm` renders correctly for modal overlay on all target browsers (modern Chrome/Firefox/Safari) | Modal Pattern | Overlay appears without blur; acceptable fallback — darkened bg still works |

---

## Open Questions

1. **Modal image aspect ratio on tall/portrait product images**
   - What we know: Some product images may be portrait-oriented (the `.jpg` files are unstandardized shots). `aspect-square` on the modal image will crop them.
   - What's unclear: Whether user wants full image visible (which would mean `object-contain` + dark padding) or cropped fill (`object-cover`).
   - Recommendation: Use `object-cover` with `aspect-square` per CLAUDE.md card pattern. If important detail is cropped, user can request `object-contain` in Phase 3 QA.

2. **Zalo SVG icon path**
   - What we know: Lucide Icons does not include Zalo or Facebook brand icons (it has no brand/social icons set). [ASSUMED — Lucide library scope knowledge from training]
   - What's unclear: Should we use a simple letter "Z" text treatment vs. the actual Zalo brand mark SVG?
   - Recommendation: Use a simple clean SVG letter icon for Zalo (angular style, 24×24) and the standard Facebook "f" SVG path. Both are freely available as inline SVG snippets — Claude can draft these at implementation time.

---

## Validation Architecture

`nyquist_validation: false` in `.planning/config.json` — this section is omitted per config.

---

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| JS masonry libraries (Masonry.js) | CSS grid `col-span-2` for gallery asymmetry | 2022+ | No JS dependency, simpler |
| CSS `columns` for waterfall layouts | CSS grid with explicit spans | 2020+ | Better row-order control |
| Native CSS masonry (`grid-template-rows: masonry`) | NOT production-ready; use grid spans | Spec 2025, no stable browser support | Don't use for this site |
| Modal libraries (Bootstrap, micromodal) | 20-line Vanilla JS toggle | All browsers support | No dependency needed |

---

## Sources

### Primary (HIGH confidence)
- `index.html` (direct read, lines 1–159) — confirmed all Tailwind tokens, section IDs, existing script block, footer content
- `CLAUDE.md` (direct read) — confirmed all design system rules, card/button/gallery patterns
- `.planning/phases/02-products-about-contact/02-CONTEXT.md` (direct read) — all D-01 through D-09 decisions
- PowerShell `Get-ChildItem images/` — confirmed all 12 image files present with correct extensions

### Secondary (MEDIUM confidence)
- [Tailwind CSS v3 Grid Template Columns docs](https://v3.tailwindcss.com/docs/grid-template-columns) — `grid-cols-4`, `col-span-2`, arbitrary values confirmed
- [MDN Masonry Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Masonry_layout) — confirms native masonry is behind flags, not production-ready
- [Can I use — masonry](https://caniuse.com/?search=masonry) — browser support data

### Tertiary (LOW confidence / ASSUMED)
- Vanilla JS modal pattern (training knowledge; verified structurally correct via multiple web results)
- Zalo brand icon availability in Lucide (training knowledge — Lucide's icon scope)

---

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — all confirmed from direct file reads; zero new packages
- Architecture patterns: HIGH — direct inspection of `index.html` confirms exact integration points
- Pitfalls: HIGH — most come from direct code analysis; masonry pitfall confirmed via MDN
- Product data: HIGH — verbatim from CONTEXT.md, file existence verified

**Research date:** 2026-05-22
**Valid until:** 2026-06-22 (stable — no external dependencies; only changes if CLAUDE.md or index.html are modified between research and planning)
