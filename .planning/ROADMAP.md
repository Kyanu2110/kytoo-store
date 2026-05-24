# ROADMAP — KYTOO.GG v1

**3 phases** | **14 requirements mapped** | All v1 requirements covered ✓

| # | Phase | Goal | Requirements | Plans |
|---|-------|------|--------------|-------|
| 1 | Core Layout & Hero | Landing page có cấu trúc HTML hoàn chỉnh, hero section đẹp | HERO-01–04, TECH-01–02 | 2 |
| 2 | Products, About & Contact | Toàn bộ content sections với ảnh thật và Shopee links | PROD-01–03, ABOUT-01–03, CONTACT-01 | 2 |
| 3 | Deploy & Verify | Site live trên URL công khai, mọi Shopee link hoạt động | TECH-03 | 1 |

---

### Phase 1: Core Layout & Hero

**Goal:** Build skeleton HTML + hero section — mở file trong browser thấy ngay landing page có hồn, responsive trên mobile.

**Requirements:**
- HERO-01: Ảnh nền Valorant fullscreen với overlay
- HERO-02: Logo + tên KYTOO.GG trên hero
- HERO-03: Tagline ngắn
- HERO-04: Nút CTA → Shopee
- TECH-01: Responsive mobile-first
- TECH-02: Single-file index.html + Tailwind CDN + Vanilla JS

**Plans:** 2 plans

Plans:
- [x] 01-01-PLAN.md — HTML skeleton: Tailwind CDN, custom color tokens, Google Fonts, fixed navbar with symmetric layout + mobile hamburger, 4 section placeholders, footer
- [x] 01-02-PLAN.md — Hero section: VALORANT_Jett_Red_1_1.webp fullscreen background, gradient overlay, Rajdhani Bold "KYTOO" heading, tagline, smooth-scroll CTA button

**Success Criteria:**
1. Mở `index.html` trong browser thấy hero fullscreen với ảnh Valorant và overlay tối
2. Logo KYTOO.GG và tagline hiển thị rõ ràng, đọc được
3. Nút CTA "Mua ngay" render đúng vị trí và màu sắc
4. Navbar sticky hiển thị logo và navigation links
5. Layout không vỡ trên 320px (mobile nhỏ nhất)

---

### Phase 2: Products, About & Contact

**Goal:** Điền đầy đủ content: grid sản phẩm với ảnh thật, modal popup, about section thuyết phục, contact links — trang hoàn chỉnh để review.

**Requirements:**
- PROD-01: Grid card hiển thị ảnh, tên, giá
- PROD-02: Nút "Mua trên Shopee" riêng từng sản phẩm
- PROD-03: Modal/popup chi tiết khi click
- ABOUT-01: Mô tả thương hiệu KYTOO.GG
- ABOUT-02: UVP — lý do chọn KYTOO
- ABOUT-03: Số liệu uy tín
- CONTACT-01: Icon/link Zalo & Facebook

**Plans:** 2 plans

Plans:
- [x] 02-01-PLAN.md — Product grid: 12 article cards (2→4 col responsive), onclick modal, PRODUCTS JS object, openModal/closeModal/Escape listener, modal element inserted before </body>
- [x] 02-02-PLAN.md — Gallery + About + Contact + Footer: col-span-2 gallery grid, brand copy + 1.000+ / 4.8★ stats, Zalo/FB contact cards, footer social icons + 2025 copyright

**Success Criteria:**
1. Grid sản phẩm hiển thị đầy đủ 12 ảnh + tên + giá, responsive grid (2 cột mobile, 4 cột desktop)
2. Click vào card sản phẩm → modal popup mở ra với ảnh lớn + mô tả
3. Click nút "Mua trên Shopee" → mở tab mới đến link Shopee (placeholder link đúng format)
4. About section có UVP + số liệu uy tín hiển thị rõ
5. Icon Zalo và Facebook trong contact section và footer, click hoạt động

---

### Phase 3: Deploy & Verify

**Goal:** Site live trên URL công khai, tất cả Shopee links được điền đúng và hoạt động, mobile check thực tế.

**Requirements:**
- TECH-03: Deploy tĩnh — GitHub Pages / Netlify

**Plans:** 1 plan

Plans:
- [x] 03-01-PLAN.md — Gitignore + asset staging, GitHub repo + Pages setup, collect 12 Shopee URLs, fill all placeholders, final QA on live URL

**Success Criteria:**
1. Site live trên URL công khai (GitHub Pages hoặc Netlify)
2. Tất cả nút "Mua trên Shopee" dẫn đến đúng listing Shopee tương ứng
3. Test trên Chrome mobile thực tế — không có layout bug nào
4. Tất cả ảnh load được từ URL public (không bị broken image)
