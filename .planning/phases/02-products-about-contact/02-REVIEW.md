---
phase: 02-products-about-contact
reviewed: 2026-05-22T17:26:12Z
depth: standard
files_reviewed: 1
files_reviewed_list:
  - index.html
findings:
  critical: 0
  warning: 5
  info: 4
  total: 9
status: issues_found
---

# Phase 02: Code Review Report

**Reviewed:** 2026-05-22T17:26:12Z
**Depth:** standard
**Files Reviewed:** 1
**Status:** issues_found

## Summary

Reviewed the single-file `index.html` after Phase 2 additions: 12-product card grid, vanilla JS modal (open/close/Escape/overlay-click), gallery grid, About section, Contact cards, and updated footer.

The implementation is largely functional. No critical security vulnerabilities or data-loss bugs were found. However, five warning-level defects exist that produce broken or incorrect behavior in predictable real-world scenarios: a gallery layout fracture on mobile, a modal that cannot be opened by keyboard users, a body scroll-lock leak when the Escape key closes the modal, redundant DOM queries inside the modal open function, and an `aria-label` typo on the close button. Four info-level quality items complete the findings.

---

## Warnings

### WR-01: Gallery `col-span-2` breaks layout on 2-column mobile grid

**File:** `index.html:155-163`
**Issue:** The gallery grid uses `grid-cols-2` as its base (mobile) breakpoint. Two cells are marked `col-span-2` (lines 156 and 163). On a 2-column grid a `col-span-2` cell works, but the remaining 10 single-column cells cannot form symmetric rows alongside it — the second `col-span-2` block (line 163) arrives mid-sequence after the 3-column and 4-column breakpoints rearrange preceding cells. On the `md` (3-column) breakpoint, `col-span-2` still spans 2 of 3 columns leaving a 1-column remainder cell on the same row, producing an orphan square next to the wide landscape cell. The layout is only clean at `lg` (4 columns) where the span-2 cells exactly halve the row. Below `lg` the asymmetry is a visible layout fracture, not a style preference.

**Fix:** Add responsive span overrides so the wide cells only span on `lg` and above:
```html
<!-- Replace col-span-2 with lg:col-span-2 on lines 156 and 163 -->
<div class="lg:col-span-2 aspect-video overflow-hidden">...</div>
```
On mobile (2-col) and md (3-col), the wide cells will render as normal single cells, which is clean. The featured wide-format at lg+ is preserved.

---

### WR-02: Product cards not keyboard-accessible — `onclick` on non-interactive `<article>` element

**File:** `index.html:97-144`
**Issue:** All 12 product cards are `<article>` elements with `onclick="openModal('...')"`. An `<article>` element has no implicit keyboard role and is not in the tab order. A user navigating by keyboard (Tab key) will never focus these cards and cannot activate them with Enter/Space. The `cursor-pointer` CSS class has no effect on keyboard accessibility. This means the modal is completely unreachable without a mouse.

**Fix:** Add `tabindex="0"` and a `keydown` handler so Enter/Space activate the modal, or replace `<article>` with `<button>` (which is natively focusable and keyboard-activatable). The button approach is simpler and semantically correct for an action trigger:
```html
<!-- Option A: keep article, add keyboard attributes -->
<article tabindex="0"
  onkeydown="if(event.key==='Enter'||event.key===' '){openModal('mysterybox');}"
  onclick="openModal('mysterybox')" ...>

<!-- Option B (preferred): use a button wrapper -->
<button type="button" onclick="openModal('mysterybox')"
  class="bg-kytoo-bg-alt border border-kytoo-border w-full text-left cursor-pointer
         transition-all duration-200 hover:border-kytoo-red hover:scale-105">
  ...
</button>
```

---

### WR-03: Escape key closes modal regardless of open state, leaking body scroll lock

**File:** `index.html:369-371`
**Issue:** The `keydown` listener at line 369 calls `closeModal()` unconditionally whenever Escape is pressed — it does not check whether the modal is actually open. `closeModal()` always executes `document.body.style.overflow = ''`, which is harmless. However, if the user opens the modal, then the Escape key fires `closeModal()` and correctly removes `overflow: hidden`. But there is a second issue: if `closeModal()` is called while the modal is already hidden (e.g., user presses Escape twice, or while no modal was ever opened), `document.body.style.overflow` is still reset. This is functionally benign in isolation but becomes a real bug if any other component also sets `body.style.overflow = 'hidden'` — the Escape key on the product modal would silently unlock the body scroll for that other component.

For this single-page site the current risk is low, but the pattern is fragile. The more immediate concrete bug is that pressing Escape when the modal is closed still calls `document.getElementById('product-modal')` (inside `closeModal`) and mutates the DOM — a wasted operation on every Escape keystroke across the entire session.

**Fix:** Guard the handler against calling close when the modal is already hidden:
```js
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') {
    const modal = document.getElementById('product-modal');
    if (modal && !modal.classList.contains('hidden')) {
      closeModal();
    }
  }
});
```

---

### WR-04: `openModal` queries the same DOM elements redundantly on every call

**File:** `index.html:348-354`
**Issue:** Every call to `openModal()` executes six separate `document.getElementById()` calls — `modal-img` is queried twice (lines 348 and 349). While `getElementById` is fast, querying the same static element twice in the same function call is an unambiguous code defect: if the `id` is ever renamed, the bug will manifest silently at runtime on one of the two lookups while the other may still work, making it harder to diagnose.

**Fix:** Cache the `modal-img` reference in a local variable:
```js
function openModal(productId) {
  const p = PRODUCTS[productId];
  if (!p) return;
  const img = document.getElementById('modal-img');
  img.src = p.img;
  img.alt = p.name;
  document.getElementById('modal-name').textContent = p.name;
  document.getElementById('modal-price').textContent = p.price;
  document.getElementById('modal-desc').textContent = p.desc;
  document.getElementById('modal-shopee-link').href = p.shopee;
  document.getElementById('product-modal').classList.remove('hidden');
  document.body.style.overflow = 'hidden';
}
```

---

### WR-05: Close button `aria-label` is untranslated ASCII ("Dong")

**File:** `index.html:376`
**Issue:** The modal close button has `aria-label="Dong"`. This is a romanized transcription of the Vietnamese word "Đóng" without the diacritic — it is not a valid English word and not properly spelled Vietnamese. Screen readers will announce this label literally as the English word "dong" (a meaningless or offensive word in English) rather than the intended "close". This is a functional accessibility error, not a style preference.

**Fix:**
```html
<button onclick="closeModal()" ... aria-label="Đóng">
```
Or use the unambiguous English label if a single-language label is preferred:
```html
<button onclick="closeModal()" ... aria-label="Close">
```

---

## Info

### IN-01: `backdrop-blur-sm` on modal overlay is not in the design system

**File:** `index.html:374`
**Issue:** The modal backdrop uses `backdrop-blur-sm`. CLAUDE.md's design system does not list blur as an approved treatment. The Valorant aesthetic is high-contrast and sharp — blur softens the background in a way that is out of character with the design language. This is a design-system violation, not a style preference.

**Fix:** Remove `backdrop-blur-sm`. The `bg-kytoo-bg/80` dark overlay already provides sufficient visual separation:
```html
<div id="product-modal" class="hidden fixed inset-0 z-[100] flex items-center justify-center bg-kytoo-bg/80" onclick="handleModalOverlayClick(event)">
```

---

### IN-02: Modal Shopee button has stale placeholder text "Mua tren Shopee"

**File:** `index.html:384`
**Issue:** The button label reads "Mua tren Shopee" — missing the diacritic on "trên". Every other label in the file uses properly accented Vietnamese. This is a copy inconsistency that will be visible to Vietnamese users.

**Fix:**
```html
<a id="modal-shopee-link" ...>Mua trên Shopee</a>
```

---

### IN-03: Product card grid missing `md:` breakpoint — jumps from 2 to 4 columns

**File:** `index.html:96`
**Issue:** The product grid uses `grid-cols-2 lg:grid-cols-4` with no `md:` intermediate step. On medium-width screens (768px–1023px, e.g., tablet portrait) the grid remains at 2 columns, making each card very wide. The gallery section at line 155 does use `md:grid-cols-3` for a smoother step. The product grid could benefit from `md:grid-cols-3` as well for visual consistency.

**Fix:**
```html
<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
```

---

### IN-04: `document.addEventListener('click', ...)` global outside-nav dismissal re-queries `nav` on every click

**File:** `index.html:251-255`
**Issue:** The global click listener that closes the mobile menu on outside-click calls `document.querySelector('nav')` on every single click event anywhere on the page. `querySelector` performs a DOM traversal each time. The `nav` element reference should be cached at setup time alongside the other cached references at lines 238-239.

**Fix:**
```js
const hamburgerBtn = document.getElementById('hamburger-btn');
const mobileMenu = document.getElementById('mobile-menu');
const navEl = document.querySelector('nav');  // cache once

// ...
document.addEventListener('click', function(e) {
  if (!navEl.contains(e.target)) {
    mobileMenu.classList.add('hidden');
  }
});
```

---

_Reviewed: 2026-05-22T17:26:12Z_
_Reviewer: Claude (gsd-code-reviewer)_
_Depth: standard_
