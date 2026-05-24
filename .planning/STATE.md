# STATE — KYTOO.GG

## Project Reference

See: .planning/PROJECT.md (updated 2026-05-22)

**Core value:** Khách truy cập web → thấy sản phẩm đẹp → click link Shopee → mua được hàng.
**Current focus:** Layout polish — gaming effects + font + content updates

## Milestone

**v1 Launch** — Landing page live với Shopee links

## Phase Status

| Phase | Name | Status |
|-------|------|--------|
| 1 | Core Layout & Hero | Complete ✓ |
| 2 | Products, About & Contact | Complete ✓ |
| 3 | Deploy & Verify | Complete ✓ |

## Current Phase

**Phase 3: Deploy & Verify** — Complete ✓ 2026-05-24

## Extra Work (ngoài plan — Phase 1 & 2)

- [x] Carousel ảnh chi tiết — mỗi sản phẩm có nhiều ảnh trong modal (auto-detect `_N.jpg`)
- [x] Scroll reveal animation — Intersection Observer, fade + slide-up, stagger theo cột
- [x] Video background hero + 4 sections
- [x] Section headings redesign — thick red bar, text-5xl, số thứ tự 01–04
- [x] Contact cards redesign — vertical layout, icon đỏ 32px, hover fill đỏ

## Layout Polish (2026-05-24 — session hiện tại)

- [x] Scanline overlay toàn trang — CSS repeating-gradient, 4% opacity, fixed z-index 9998
- [x] Glitch animation — hero h1 (5s interval) + navbar logo (8s, delay 3s)
- [x] Moving scan line đỏ trong hero section — 7s linear loop
- [x] Red glow hover trên 12 product cards — box-shadow 22px rgba(255,70,85,0.28)
- [x] Section numbers 01–04 pulse animation — 4s ease-in-out
- [x] CTA button glow hover — box-shadow 18px
- [x] Font VALORANT cho hero h1 — local file `fonts/Valorant Font.ttf` via @font-face
  - font-size: clamp(5rem, 22vw, 18rem), letter-spacing 0.08em
  - Căn giữa viewport bằng `width:100vw; left:50%; margin-left:-50vw`
- [x] Font Be Vietnam Pro cho section headings — Google Fonts, hỗ trợ tiếng Việt đầy đủ
  - Token `font-heading` trong Tailwind config
  - Áp dụng cho 4 section h2 (thay Rajdhani không có tiếng Việt)
- [x] Nội dung Về KYTOO — rewrite 5 đoạn mới (fan-first tone)
- [x] Stats Về KYTOO — cập nhật số liệu thật từ Shopee & TikTok
  - Shopee: 1,2K followers · 4.9★ (353 đánh giá)
  - TikTok: 11,3K followers · 310,6K lượt thích
  - Layout: 2 platform, mỗi platform 2 chỉ số, căn giữa trong cột phải

## Next Step

**v1 Launch Complete** — Site live tại https://kyanu2110.github.io/kytoo-store/

Các hướng tiếp theo (v2):
- Custom domain (kytoo.gg / kytoo.vn)
- Google Analytics
- SEO / Open Graph tags
- Shopee links cho tactical + wingman khi có listing

## Notes

- Font file: `fonts/Valorant Font.ttf` (local, không dùng CDN)
- Ảnh sản phẩm: `images/` — 12 ảnh chính + ảnh chi tiết
- Shopee links cần điền thật ở Phase 3
- Không có build step — mọi thứ trong `index.html`
