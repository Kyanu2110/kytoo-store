---
plan: 02-01
phase: 02-products-about-contact
status: complete
completed: 2026-05-23
commit: ccddf29
---

# Plan 02-01 Summary: Product Grid + Modal Popup

## What Was Built

Replaced the `#san-pham` placeholder stub with a fully functional 12-product shopping section:

**Product Grid (Task 1):**
- 12 `<article>` cards in a responsive grid: `grid-cols-2` mobile → `lg:grid-cols-4` desktop
- Each card: `aspect-square` product image, `line-clamp-2` full Vietnamese product name, price in `text-kytoo-red`
- Cards ordered price-descending per D-03
- Hover effect: `hover:border-kytoo-red hover:scale-105` — angular, no `rounded-*`
- `onclick="openModal('{key}')"` on each card — all 12 wired

**Modal Popup (Task 2):**
- `<div id="product-modal">` added before `</body>` with `hidden` default, `z-[100]` (above z-50 navbar)
- Inner card: `stopPropagation` prevents overlay-click from firing inside card
- Three close paths: X button (`closeModal()`), overlay click (`handleModalOverlayClick`), Escape key
- Body scroll locked on open (`overflow: hidden`), restored on close
- Shopee button with `target="_blank" rel="noopener"`, placeholder `#shopee-{key}` hrefs

**PRODUCTS data object:**
- 12 entries with `name`, `price`, `img`, `desc`, `shopee` fields
- `nhandaychuyen` correctly uses `images/nhandaychuyen.png` (not .jpg)
- Descriptions: 1-2 sentence Vietnamese Claude drafts from RESEARCH.md
- Appended to existing `<script>` block — no new `<script>` tag

## Verification Results

| Check | Expected | Actual | Status |
|-------|----------|--------|--------|
| `grep -c onclick="openModal("` | 12 | 12 | ✓ |
| `grep -c "article"` | 24 | 24 | ✓ |
| `grep -c "rounded-"` | 0 | 0 | ✓ |
| `grep "nhandaychuyen"` | .png extension | .png (both card + PRODUCTS) | ✓ |
| `grep -c "id=\"product-modal\""` | 1 | 1 | ✓ |
| `grep -c "function openModal"` | 1 | 1 | ✓ |
| `grep -c "function closeModal"` | 1 | 1 | ✓ |
| `grep -c "Escape"` | 1 | 1 | ✓ |
| `grep "z-\[100\]"` | present | z-[100] on modal div | ✓ |

Note: `grep -c "<script"` = 3 (CDN script + Tailwind config + JS block). Plan expected 2 but didn't count the CDN script tag on line 10. No new script tag was added — this is correct behavior.

## Key Files

- `index.html` — product grid (12 articles) + modal overlay + PRODUCTS JS object + modal functions

## Self-Check: PASSED
