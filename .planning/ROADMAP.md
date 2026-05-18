# KYTOO.GG — Roadmap v1

**Project:** KYTOO.GG Valorant Merch Store VN
**Milestone:** v1 Launch — biến landing page thành store hoạt động thật sự

---

## Phases

### Phase 1: Sản phẩm thật + Shopee Links

**Goal:** Người dùng có thể xem hình ảnh thật của sản phẩm và click mua ngay trên Shopee
**Mode:** mvp

**Requirements:** PROD-01, PROD-02

**Plans:** 2 plans in 2 waves

**Wave 1**
- [ ] `01-01` — Collect product data + replace all placeholders with real products across 3 sections

**Wave 2** *(blocked on Wave 1 completion)*
- [ ] `01-02` — Audit remaining Shopee link gaps + final browser sign-off

**Cross-cutting constraints:**
- All href values on Shopee CTAs: hardcoded `https://shopee.vn/...` string literals only
- All product `<img>` tags: `onerror` gradient fallback (exact literal per D-12)
- Only `index.html` modified (+ `images/.gitkeep`)

**Success Criteria:**
1. Đủ 15 sản phẩm thật hiển thị trên trang — section #all-products (grid catalog mới) hiển thị cả 15; featured carousel, agent tabs spotlight (5–8 SP nổi bật), và collection slider đều có ảnh thật (hoặc đúng slot để thêm ảnh)
2. Tất cả nút "Mua ngay" / "Xem trên Shopee" có link thật đến Shopee listing (hoặc shop page nếu chưa có listing riêng)
3. Tên và giá sản phẩm khớp với Shopee

**Status:** Planned

---

### Phase 2: Form liên hệ thật

**Goal:** Người dùng submit form → KYTOO nhận được email
**Mode:** mvp

**Requirements:** CONTACT-01

**Success Criteria:**
1. Form tích hợp Formspree (hoặc EmailJS) — submit gửi email đến địa chỉ cấu hình
2. Hiển thị success message khi gửi thành công
3. Hiển thị error message khi gửi thất bại
4. Không cần backend — pure frontend integration

**Status:** Pending

---

### Phase 3: Google Analytics

**Goal:** Team có data về traffic và hành vi người dùng
**Mode:** mvp

**Requirements:** TRACK-01

**Success Criteria:**
1. GA4 tracking code được gắn đúng cách trong `<head>`
2. Pageview được track tự động
3. Click vào các CTA "Shopee" được track là events
4. Không ảnh hưởng đến performance (async loading)

**Status:** Pending

---

### Phase 4: SEO + Open Graph

**Goal:** Site hiển thị đẹp khi share và có thể được Google index
**Mode:** mvp

**Requirements:** SEO-01

**Success Criteria:**
1. `<title>` và `<meta name="description">` được điền đúng và unique
2. Open Graph tags đầy đủ: `og:title`, `og:description`, `og:image`, `og:url`, `og:type`
3. Twitter Card meta tags
4. `og:image` là ảnh thật (không phải placeholder), kích thước 1200×630px
5. Kiểm tra được qua Facebook Sharing Debugger hoặc opengraph.io

**Status:** Pending

---

### Phase 5: Performance — Lazy Loading

**Goal:** Trang tải nhanh hơn — chỉ load ảnh khi cần
**Mode:** mvp

**Requirements:** PERF-01

**Success Criteria:**
1. Tất cả `<img>` tags có `loading="lazy"` attribute
2. Above-the-fold images (hero) giữ `loading="eager"` hoặc không set (không lazy)
3. LCP (Largest Contentful Paint) không bị tăng so với baseline
4. Có thể test bằng Chrome DevTools Network throttling

**Status:** Pending

---

### Phase 6: Deploy Ready

**Goal:** Site sẵn sàng deploy lên static hosting và có favicon
**Mode:** mvp

**Requirements:** DEPLOY-01

**Success Criteria:**
1. Favicon.ico và favicon.png (32×32, 180×180) tồn tại trong root
2. `<link rel="icon">` và `<link rel="apple-touch-icon">` được gắn đúng trong `<head>`
3. `netlify.toml` hoặc `vercel.json` cơ bản được tạo (hoặc README hướng dẫn deploy GitHub Pages)
4. `.gitignore` phù hợp
5. Git có ít nhất 1 commit với toàn bộ code

**Status:** Pending

---

## Coverage

| REQ-ID | Phase | Description |
|--------|-------|-------------|
| PROD-01 | Phase 1 | Hình ảnh thật cho sản phẩm |
| PROD-02 | Phase 1 | Link Shopee cho tất cả CTA |
| CONTACT-01 | Phase 2 | Form liên hệ gửi email thật |
| TRACK-01 | Phase 3 | Google Analytics 4 |
| SEO-01 | Phase 4 | Meta tags + Open Graph |
| PERF-01 | Phase 5 | Lazy loading hình ảnh |
| DEPLOY-01 | Phase 6 | Favicon + deploy config |

**6 phases | 7 requirements | 100% v1 requirements covered ✓**
