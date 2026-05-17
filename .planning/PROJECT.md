# KYTOO.GG — Valorant Merch Store VN

## What This Is

KYTOO.GG là shop bán đồ lưu niệm Valorant chính hãng tại Việt Nam — quần áo, phụ kiện gaming, collectibles theo nhân vật. Landing page đã hoàn chỉnh với design Valorant tactical aesthetic. Bước tiếp theo là biến landing page thành một store hoạt động thật sự: hình ảnh sản phẩm thật, link mua hàng qua Shopee, form liên hệ hoạt động, và SEO cơ bản.

## Core Value

Người xem landing page phải có thể tìm và mua sản phẩm ngay — click vào sản phẩm là ra trang Shopee mua được.

## Requirements

### Validated

- ✓ Landing page UI hoàn chỉnh — Hero, Products, About, Agent Gear tabs, Collection, Gallery, Contact — existing
- ✓ Responsive design (desktop + mobile) — existing
- ✓ Valorant tactical aesthetic (clip-path, colors, typography) — existing
- ✓ JavaScript interactions (carousels, agent tabs, scroll-to-top, mobile nav) — existing

### Active

- [ ] Hình ảnh sản phẩm thật thay placeholder/gradient
- [ ] Link Shopee thật gắn vào tất cả nút "Mua ngay" / "Xem trên Shopee"
- [ ] Form liên hệ gửi email thật (Formspree hoặc EmailJS)
- [ ] SEO cơ bản: meta tags, Open Graph, favicon
- [ ] Google Analytics / tracking cơ bản
- [ ] Tốc độ tải trang (optimize images, lazy loading)
- [ ] Trang 404 và error states

### Out of Scope

- Giỏ hàng riêng — dùng Shopee làm kênh bán hàng, không tự làm cart
- Backend/database riêng — static site, không cần server
- Hệ thống tài khoản user — không cần auth cho v1
- Blog/CMS — không trong scope đầu

## Context

**Tech stack hiện tại:** Single-file HTML (1542 dòng), Tailwind CSS CDN, Lucide icons, Google Fonts (Rajdhani + Inter), Vanilla JS thuần. Không có build system, không có framework.

**Kênh bán hàng:** Shopee — landing page dùng làm showcase + drive traffic đến Shopee shop. Nhiều CTA "Xem trên Shopee" đã có trong UI nhưng chưa có link thật.

**Sản phẩm hiện có trong UI (placeholder):**
- Jett Windslash Hoodie — 350.000₫
- Reyna Devour Keycap Series — 280.000₫
- Sage Healing Art Print — 120.000₫
- Neon Sprint Mug — 150.000₫
- Killjoy Lab Mousepad — 420.000₫

**File duy nhất:** `index.html` + 1 ảnh `bef937a7b661a05103b38a4e57ffb195.jpg`

**Git:** Initialized, chưa có commit nào.

## Constraints

- **Tech stack**: Giữ nguyên static HTML — không thêm build system hay framework phức tạp
- **Kênh bán**: Shopee là kênh duy nhất — không tự build checkout
- **Hosting**: Phù hợp với static hosting (GitHub Pages, Netlify, Vercel)
- **Timeline**: Ưu tiên ship nhanh — hoàn thiện cái đang có trước khi thêm feature mới

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Dùng Shopee làm kênh bán | Không cần tự build payment, trust sẵn có | — Pending |
| Giữ single-file HTML | Đơn giản, deploy dễ, không cần server | — Pending |
| Formspree/EmailJS cho form | Static site cần third-party form service | — Pending |

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
*Last updated: 2026-05-17 after initialization*
