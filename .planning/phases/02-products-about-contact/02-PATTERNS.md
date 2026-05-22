# Phase 2: Products, About & Contact — Pattern Map

**Mapped:** 2026-05-23
**Files analyzed:** 1 (index.html — single-file project; all changes target this file)
**Analogs found:** all patterns extracted from index.html directly (no external analogs needed)

---

## File Classification

| Target Structure | Role | Data Flow | Closest Analog in index.html | Match Quality |
|-----------------|------|-----------|------------------------------|---------------|
| `#san-pham` product grid | component (section content) | request-response (click → modal) | Navbar CTA button (button pattern), Hero section (section wrapper pattern) | role-match |
| Product card (×12) | component (card) | event-driven (onclick → openModal) | No card exists yet — pattern from CLAUDE.md + RESEARCH.md | design-system match |
| `#product-modal` overlay | component (modal) | event-driven (open/close via JS) | No modal exists yet — pattern from RESEARCH.md | new pattern |
| `#bo-suu-tap` gallery | component (section content) | static render | `#san-pham` section wrapper (same outer shell) | exact |
| `#ve-kytoo` about | component (section content) | static render | `#san-pham` section wrapper (same outer shell) | exact |
| `#lien-he` contact | component (section content) | static render | `#san-pham` section wrapper (same outer shell) | exact |
| `<footer>` update | component (footer) | static render | Existing `<footer>` lines 131–135 | exact |
| Modal JS + product data | service (client-side) | event-driven | Hamburger JS block lines 137–157 | role-match |

---

## Pattern Assignments

### Section Wrapper Pattern

**Source:** `index.html` lines 90–98 (`#san-pham`), 100–108 (`#bo-suu-tap`), 110–118 (`#ve-kytoo`), 120–128 (`#lien-he`)

All 4 sections share the identical outer shell. The only differences are: section `id`, background class (`bg-kytoo-bg` vs `bg-kytoo-bg-alt`), and heading text.

**Exact outer shell (lines 90–98 — `#san-pham` as canonical):**
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

**Background alternation (confirmed from index.html):**
- `#san-pham` → `bg-kytoo-bg` (line 90)
- `#bo-suu-tap` → `bg-kytoo-bg-alt` (line 100)
- `#ve-kytoo` → `bg-kytoo-bg` (line 110)
- `#lien-he` → `bg-kytoo-bg-alt` (line 120)

**Integration rule:** Replace only `<p class="text-kytoo-gray text-sm">— Phase 2 content —</p>` on lines 96, 106, 116, 126. Keep the `<div class="flex items-center gap-2 mb-4">` heading row untouched.

---

### Section Heading Pattern

**Source:** `index.html` lines 92–95 (same in all 4 sections)

```html
<div class="flex items-center gap-2 mb-4">
  <span class="w-8 h-0.5 bg-kytoo-red inline-block"></span>
  <h2 class="text-3xl font-display font-bold uppercase tracking-widest text-kytoo-cream">Sản Phẩm</h2>
</div>
```

This heading block is ALREADY PRESENT in all 4 sections — do not re-add it, only replace the placeholder `<p>` that follows it.

---

### Primary Button / CTA Pattern

**Source:** `index.html` line 54 (navbar CTA) and line 85 (hero CTA)

**Navbar CTA (line 54) — compact variant:**
```html
<a href="#shopee-placeholder" class="bg-kytoo-red text-white uppercase tracking-widest px-6 py-2 text-sm font-semibold hover:bg-kytoo-red-dark transition-colors">Mua ngay</a>
```

**Hero CTA (line 85) — large variant:**
```html
<a href="#san-pham" class="inline-block bg-kytoo-red text-white uppercase tracking-widest px-10 py-4 font-body font-semibold text-sm hover:bg-kytoo-red-dark transition-colors">Khám phá sản phẩm</a>
```

**Modal "Mua trên Shopee" button (from RESEARCH.md — new instance):**
```html
<a id="modal-shopee-link" href="#shopee-placeholder" target="_blank" rel="noopener"
   class="block text-center bg-kytoo-red text-white uppercase tracking-widest px-8 py-3 text-sm font-semibold hover:bg-kytoo-red-dark transition-colors">
  Mua trên Shopee
</a>
```

**Critical constraints (all instances):**
- NO `rounded-*` class anywhere — zero instances in existing code, enforce strictly
- `hover:bg-kytoo-red-dark` for hover state (not `hover:opacity-*`)
- `transition-colors` for transition (not `transition` or `transition-all`)
- `uppercase tracking-widest` always present

---

### Nav Link Pattern (secondary use — contact cards hover)

**Source:** `index.html` lines 43–44 (desktop nav links)

```html
<a href="#san-pham" class="text-kytoo-cream text-sm uppercase tracking-widest hover:text-kytoo-red transition-colors">Sản phẩm</a>
```

Contact section link cards borrow this hover-colors pattern extended to border:
```
hover:border-kytoo-red transition-colors
```

---

### Product Card Pattern

**Source:** RESEARCH.md Pattern 1 (no card exists yet in index.html — this is the first instance)

```html
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

**Key constraints:**
- `onclick="openModal('{productKey}')"` — productKey matches keys in PRODUCTS JS object
- `aspect-square` on the image wrapper — enforces uniform card height regardless of source image dimensions
- `line-clamp-2` on product name — Tailwind CDN v3.3+ built-in; no plugin needed
- NO `<a>` wrapping — modal open is via `onclick` on the outer `<div>`
- `rounded-none` is NOT written — absence of `rounded-*` is the default; adding `rounded-none` is unnecessary

---

### Product Grid Pattern

**Source:** RESEARCH.md Pattern 2 (no grid exists yet in index.html)

```html
<div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
  <!-- 12 product cards -->
</div>
```

Note: `md:grid-cols-2` is redundant since base is already `grid-cols-2`. Only `lg:grid-cols-4` breakpoint is needed. Gap is `gap-4` per CLAUDE.md spacing rhythm.

---

### Modal Overlay Pattern

**Source:** RESEARCH.md Pattern 3 (no modal exists yet in index.html)

**Insertion point:** Immediately before `</body>` — after the closing `</script>` tag at line 157, before `</body>` at line 158.

```html
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

**Constraints enforced:**
- `hidden` class — toggle target for `openModal`/`closeModal`
- `z-50` — above navbar (`z-50` in nav); modal must be same or higher. Navbar is also `z-50` — modal should be `z-[60]` or `z-[100]` to guarantee it renders above the fixed navbar. Use `z-[100]`.
- `stroke-linecap="square"` on close SVG — matches hamburger icon style (line 58)
- NO `rounded-*` on inner card `<div>`

---

### JS Script Block — Insertion Point

**Source:** `index.html` lines 137–157

```javascript
// EXISTING block — do NOT create a new <script> tag
// All modal JS and PRODUCTS data object are APPENDED inside this same block
// before the closing </script> at line 157

const hamburgerBtn = document.getElementById('hamburger-btn');
const mobileMenu   = document.getElementById('mobile-menu');

hamburgerBtn.addEventListener('click', function() {
  mobileMenu.classList.toggle('hidden');
});

mobileMenu.querySelectorAll('a').forEach(function(link) {
  link.addEventListener('click', function() {
    mobileMenu.classList.add('hidden');
  });
});

document.addEventListener('click', function(e) {
  const nav = document.querySelector('nav');
  if (!nav.contains(e.target)) {
    mobileMenu.classList.add('hidden');
  }
});

// ↑ END OF EXISTING CODE
// ↓ APPEND modal JS here — within the same <script> block
```

**Modal JS pattern to append (RESEARCH.md Pattern 4):**

```javascript
const PRODUCTS = {
  mysterybox:    { name: '...', price: '150.000₫ – 279.000₫', img: 'images/mysterybox.jpg',    desc: '...', shopee: '#shopee-mysterybox' },
  keycapcustom:  { name: '...', price: '279.000₫',             img: 'images/keycapcustom.jpg',  desc: '...', shopee: '#shopee-keycapcustom' },
  keycap14phim:  { name: '...', price: '251.100₫ – 279.000₫', img: 'images/keycap14phim.jpg',  desc: '...', shopee: '#shopee-keycap14phim' },
  tactical:      { name: '...', price: '279.000₫',             img: 'images/tactical.jpg',      desc: '...', shopee: '#shopee-tactical' },
  wingman:       { name: '...', price: '152.100₫',             img: 'images/wingman.jpg',       desc: '...', shopee: '#shopee-wingman' },
  nhanclove:     { name: '...', price: '79.000₫',              img: 'images/nhanclove.jpg',     desc: '...', shopee: '#shopee-nhanclove' },
  nuochoa:       { name: '...', price: '69.000₫',              img: 'images/nuochoa.jpg',       desc: '...', shopee: '#shopee-nuochoa' },
  blindbox:      { name: '...', price: '67.150₫',              img: 'images/blindbox.jpg',      desc: '...', shopee: '#shopee-blindbox' },
  padchuot:      { name: '...', price: '63.200₫ – 79.000₫',   img: 'images/padchuot.jpg',      desc: '...', shopee: '#shopee-padchuot' },
  miengketay:    { name: '...', price: '55.200₫',              img: 'images/miengketay.jpg',    desc: '...', shopee: '#shopee-miengketay' },
  nhandaychuyen: { name: '...', price: '37.000₫ – 44.100₫',   img: 'images/nhandaychuyen.png', desc: '...', shopee: '#shopee-nhandaychuyen' },
  meotreomanhinh:{ name: '...', price: '35.000₫',              img: 'images/meotreomanhinh.jpg',desc: '...', shopee: '#shopee-meotreomanhinh' },
};

function openModal(productId) {
  const p = PRODUCTS[productId];
  if (!p) return;
  document.getElementById('modal-img').src       = p.img;
  document.getElementById('modal-img').alt        = p.name;
  document.getElementById('modal-name').textContent  = p.name;
  document.getElementById('modal-price').textContent = p.price;
  document.getElementById('modal-desc').textContent  = p.desc;
  document.getElementById('modal-shopee-link').href  = p.shopee;
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

**Critical:** `nhandaychuyen` uses `.png` extension — `images/nhandaychuyen.png`. All others are `.jpg`.

---

### Gallery Grid Pattern

**Source:** RESEARCH.md Pattern 5 (no gallery exists yet; CLAUDE.md Gallery Grid rules apply)

```html
<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-2">
  <!-- 2 featured cells: col-span-2 + aspect-video -->
  <div class="col-span-2 aspect-video overflow-hidden">
    <img src="images/mysterybox.jpg" alt="" class="w-full h-full object-cover" aria-hidden="true">
  </div>
  <!-- Regular cells: aspect-square -->
  <div class="aspect-square overflow-hidden">
    <img src="images/blindbox.jpg" alt="" class="w-full h-full object-cover" aria-hidden="true">
  </div>
  <!-- ... 10 more cells -->
</div>
```

**Key constraints:**
- `gap-2` (not `gap-4`) — Gallery Grid per CLAUDE.md uses `gap-1`/`gap-2`, tighter than product grid
- `aria-hidden="true"` on all gallery images — purely decorative, no text overlay
- NO text labels, NO price, NO hover CTA on gallery cells — visual only (differentiates from #san-pham)
- `col-span-2` for featured cells; `aspect-square` for regular cells
- Do NOT use `columns-*` CSS multi-column or native CSS masonry

---

### About Section Layout Pattern

**Source:** RESEARCH.md Pattern 6 (no about content exists yet; uses section wrapper + Tailwind grid)

```html
<!-- Replaces the <p class="text-kytoo-gray text-sm">— Phase 2 content —</p> on line 116 -->
<div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
  <!-- Left: brand copy -->
  <div>
    <p class="text-kytoo-cream leading-relaxed mb-4">...</p>
    <p class="text-kytoo-cream leading-relaxed">...</p>
  </div>
  <!-- Right: social proof stats -->
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

Stat number style borrows from the hero `h1` pattern (line 83): `font-display font-extrabold uppercase tracking-widest` — adapted to `font-bold text-5xl` for stats.

---

### Contact Cards + Footer Pattern

**Source:** `index.html` lines 131–135 (existing footer); RESEARCH.md Pattern 7 (contact cards)

**Existing footer (lines 131–135) — exact current state:**
```html
<footer class="bg-kytoo-bg border-t border-kytoo-border py-8">
  <div class="max-w-7xl mx-auto px-4 text-center">
    <p class="text-kytoo-gray text-sm">© 2024 KYTOO Store. All rights reserved.</p>
  </div>
</footer>
```

**Contact cards (replace placeholder in `#lien-he` section, line 126):**
```html
<div class="flex flex-col sm:flex-row gap-4">
  <a href="#zalo-placeholder" class="flex items-center gap-3 border border-kytoo-border bg-kytoo-bg-alt px-6 py-4 hover:border-kytoo-red transition-colors">
    <!-- Zalo SVG inline (24×24, letter 'Z' style) -->
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="square"><!-- path --></svg>
    <div>
      <p class="text-kytoo-cream font-semibold text-sm uppercase tracking-widest">Zalo</p>
      <p class="text-kytoo-gray text-xs">Nhắn tin trực tiếp</p>
    </div>
  </a>
  <a href="#facebook-placeholder" class="flex items-center gap-3 border border-kytoo-border bg-kytoo-bg-alt px-6 py-4 hover:border-kytoo-red transition-colors">
    <!-- Facebook SVG inline (24×24, 'f' path) -->
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><!-- path --></svg>
    <div>
      <p class="text-kytoo-cream font-semibold text-sm uppercase tracking-widest">Facebook</p>
      <p class="text-kytoo-gray text-xs">Like trang KYTOO</p>
    </div>
  </a>
</div>
```

**Footer replacement (update lines 131–135):**
```html
<footer class="bg-kytoo-bg border-t border-kytoo-border py-8">
  <div class="max-w-7xl mx-auto px-4 text-center">
    <div class="flex items-center justify-center gap-6 mb-4">
      <a href="#zalo-placeholder" class="text-kytoo-gray hover:text-kytoo-cream transition-colors" aria-label="Zalo"><!-- Zalo SVG 20×20 --></a>
      <a href="#facebook-placeholder" class="text-kytoo-gray hover:text-kytoo-cream transition-colors" aria-label="Facebook"><!-- Facebook SVG 20×20 --></a>
    </div>
    <p class="text-kytoo-gray text-sm">© 2025 KYTOO Store. All rights reserved.</p>
  </div>
</footer>
```

Note: copyright year must change from `2024` → `2025`.

---

## Shared Patterns

### Color Tokens (apply everywhere — zero exceptions)

**Source:** `index.html` lines 12–33 (Tailwind config block)

```javascript
colors: {
  'kytoo-bg':       '#0F1923',
  'kytoo-bg-alt':   '#1a2634',
  'kytoo-red':      '#FF4655',
  'kytoo-red-dark': '#BD3944',
  'kytoo-cream':    '#ECE8E1',
  'kytoo-gray':     '#768079',
  'kytoo-border':   '#2a3f52',
}
```

These tokens already exist — use `text-kytoo-red`, `bg-kytoo-bg-alt`, etc. No inline `style="color: ..."` ever.

### Typography Tokens

**Source:** `index.html` lines 24–27 (Tailwind config) + line 36 (body class)

```javascript
fontFamily: {
  display: ['Rajdhani', 'sans-serif'],   // use: font-display
  body:    ['Inter', 'sans-serif'],       // use: font-body (also default body class)
}
```

- Section headings: `font-display font-bold` (same as lines 94, 104, 114, 124)
- Body text: `font-body` or omit (body default)
- Stats / large numbers: `font-display font-bold`

### No Border-Radius Rule

**Source:** CLAUDE.md + verified absence in index.html (grep confirmed: zero `rounded-*` occurrences)

Applies to: product cards, modal container, modal inner card, all buttons, contact cards, gallery cells. No exceptions.

### SVG Stroke Style

**Source:** `index.html` lines 58–63 (hamburger icon), lines 210–212 (modal close icon from RESEARCH.md)

```html
stroke-linecap="square"  <!-- NOT "round" — maintains angular aesthetic -->
stroke-width="2"
```

All inline SVG icons must use `stroke-linecap="square"`. The close button SVG (`×`) in the modal matches this.

### Hover Transition Pattern

**Source:** `index.html` lines 43, 54, 85 (nav links and buttons)

```
hover:text-kytoo-red transition-colors     ← for text color transitions
hover:bg-kytoo-red-dark transition-colors  ← for background transitions (buttons)
hover:border-kytoo-red transition-colors   ← for border transitions (cards, contact links)
hover:scale-105 transition-all duration-200 ← for card scale + border combined
```

Product cards use `transition-all duration-200` to handle both `hover:scale-105` and `hover:border-kytoo-red` in one declaration.

---

## No Analog Found

No section of index.html currently contains a product card, modal overlay, gallery grid, or about/contact content. All four sections have identical `— Phase 2 content —` stubs. However, all patterns are fully defined by:

1. The existing `index.html` code (section wrappers, heading structure, button classes, SVG stroke style, Tailwind tokens)
2. CLAUDE.md design system rules
3. RESEARCH.md verified patterns

| Structure | Reason No Analog Exists |
|-----------|------------------------|
| Product card | First card component in project — Phase 2 introduces it |
| Modal overlay | No modal exists in project yet — Phase 2 introduces it |
| Gallery grid | No gallery exists yet — Phase 2 introduces it |
| About 2-col layout | No multi-column content section yet — Phase 2 introduces it |
| Contact link cards | No contact section content yet — Phase 2 introduces it |

All five structures have complete design-system grounding — the executor should treat RESEARCH.md patterns (which were verified against index.html) as the authoritative source.

---

## Critical Implementation Warnings

1. **Line 96, 106, 116, 126** — replace only the `<p class="text-kytoo-gray text-sm">— Phase 2 content —</p>` line in each section. The heading `<div>` above it stays.

2. **`nhandaychuyen` extension is `.png`** — not `.jpg`. Both the grid card `<img src>` and the PRODUCTS JS object must use `images/nhandaychuyen.png`.

3. **Modal z-index** — the navbar is `z-50` (line 39). The modal overlay must use `z-[100]` (or at minimum `z-[60]`) so it renders above the fixed navbar when opened.

4. **All three modal close paths** (`closeModal()` function, overlay click, Escape key) must call the same `closeModal()` function to ensure `document.body.style.overflow = ''` is always reset.

5. **Footer year** — line 133 has `© 2024`, must update to `© 2025`.

6. **Social icons** — Lucide CDN has no Zalo or Facebook brand icons. Use SVG inline only.

7. **No new `<script>` tag** — append all modal JS inside the existing `<script>` block (lines 137–157), between the last existing line (line 156 `}`) and the closing `</script>` (line 157).

---

## Metadata

**Analog search scope:** `index.html` (sole source file — single-file project per CLAUDE.md)
**Files scanned:** 1 (`index.html`, 159 lines, fully read)
**Supporting docs read:** `02-CONTEXT.md`, `02-RESEARCH.md`, `CLAUDE.md` (via system context)
**Pattern extraction date:** 2026-05-23
