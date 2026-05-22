# KYTOO.GG

## What This Is

Landing page merch Valorant tại Việt Nam — giới thiệu sản phẩm vật lý (keycap, phụ kiện, đồ lưu niệm Valorant), kết nối khách hàng đến shop Shopee của KYTOO.GG. Không tự xây cart — Shopee là kênh bán duy nhất.

## Core Value

Khách truy cập web → thấy sản phẩm đẹp → click link Shopee → mua được hàng.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Hero section với ảnh nền Valorant, tagline, CTA chính
- [ ] Grid sản phẩm nổi bật: ảnh, tên, giá, nút "Mua trên Shopee"
- [ ] About section giới thiệu thương hiệu KYTOO.GG
- [ ] Form liên hệ (Formspree hoặc tương tự)
- [ ] Deploy được, Shopee link hoạt động
- [ ] Responsive mobile-first

### Out of Scope

- Giỏ hàng / thanh toán trực tiếp — dùng Shopee thay thế
- User account / login — không cần cho v1
- CMS / admin panel — cập nhật thủ công HTML
- Build system / bundler — giữ single-file để dễ deploy

## Context

- Đã có bộ ảnh sản phẩm tại `images/`: mysterybox, blindbox, keycap14phim, keycapcustom, padchuot, wingman, tactical, nuochoa, nhanclove, nhandaychuyen, miengketay, meotreomanhinh
- Ảnh hero Valorant: `VALORANT_Jett_Red_1_1.webp` (root folder)
- Dự án trước đã xây xong index.html nhưng bị xóa — rebuild từ đầu với cấu trúc GSD rõ ràng hơn

## Constraints

- **Tech stack**: Single-file HTML + Tailwind CSS CDN + Vanilla JS — không build step, không framework
- **Deploy**: File tĩnh, có thể host trên GitHub Pages / Netlify / bất kỳ static host
- **Nội dung**: Tiếng Việt, thị trường Việt Nam
- **Bán hàng**: Shopee là kênh duy nhất — không tự build payment

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Single-file HTML | Dễ deploy, không cần build pipeline, dễ maintain | — Pending |
| Shopee thay vì tự build cart | Giảm complexity, tận dụng hạ tầng Shopee sẵn có | — Pending |
| Tailwind CDN | Không cần npm, phù hợp single-file approach | — Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `/gsd-transition`):
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active
4. Decisions to log? → Add to Key Decisions
5. "What This Is" still accurate? → Update if drifted

**After each milestone** (via `/gsd:complete-milestone`):
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-05-22 after initialization*
