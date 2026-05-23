# STATE — KYTOO.GG

## Project Reference

See: .planning/PROJECT.md (updated 2026-05-22)

**Core value:** Khách truy cập web → thấy sản phẩm đẹp → click link Shopee → mua được hàng.
**Current focus:** Phase 3 — Deploy & Verify (sẵn sàng)

## Milestone

**v1 Launch** — Landing page live với Shopee links

## Phase Status

| Phase | Name | Status |
|-------|------|--------|
| 1 | Core Layout & Hero | Complete ✓ |
| 2 | Products, About & Contact | Complete ✓ |
| 3 | Deploy & Verify | Not started |

## Current Phase

**Phase 2: Products, About & Contact** — 2 plans, 2 waves ◆ COMPLETE ✓

Plans:
- [x] 02-01 (Wave 1): Product grid (12 cards) + Vanilla JS modal
- [x] 02-02 (Wave 2): Gallery + About + Contact + Footer social links

Last Activity: 2026-05-24 — Thêm ảnh chi tiết carousel + scroll reveal animation

## Extra Work (ngoài plan)

- [x] Carousel ảnh chi tiết — mỗi sản phẩm có nhiều ảnh trong modal (auto-detect `_N.jpg`)
  - mysterybox: 24 ảnh | blindbox: 3 | keycapcustom: 4 | keycap14phim: 16
  - tactical: 6 | wingman: 6 | nhanclove: 4 | nuochoa: 12
  - padchuot: 5 | miengketay: 4 | nhandaychuyen: 4 (hardcoded PNG) | meotreomanhinh: 5
- [x] Scroll reveal animation — Intersection Observer, fade + slide-up, stagger theo cột
  - Section headings, product cards, gallery, about, contact, footer
  - Tôn trọng `prefers-reduced-motion`

## Notes

- Ảnh sản phẩm: `images/` — 12 ảnh chính + ảnh chi tiết cho từng sản phẩm
- Hero background: `VALORANT_Jett_Red_1_1.webp` (root)
- Shopee links cần điền thật ở Phase 3
- Không có build step — mọi thứ trong `index.html`
