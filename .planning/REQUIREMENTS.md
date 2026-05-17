# KYTOO.GG — Requirements v1

## v1 Requirements

### Products (PROD)

- [ ] **PROD-01**: Người dùng có thể xem hình ảnh thật của từng sản phẩm (Hoodie, Keycap, Art Print, Mug, Mousepad) thay vì placeholder/gradient
- [ ] **PROD-02**: Người dùng có thể click "Mua ngay" / "Xem trên Shopee" trên bất kỳ sản phẩm nào và được redirect đến đúng listing Shopee tương ứng

### Contact (CONTACT)

- [ ] **CONTACT-01**: Người dùng có thể điền và submit form liên hệ, và KYTOO nhận được email thật (tích hợp Formspree hoặc EmailJS)

### Tracking (TRACK)

- [ ] **TRACK-01**: Google Analytics 4 được gắn vào site để track lượng truy cập và hành vi người dùng cơ bản

### SEO (SEO)

- [ ] **SEO-01**: Site có đầy đủ meta tags và Open Graph tags để hiển thị đẹp khi share lên mạng xã hội (Facebook, Zalo, v.v.)

### Performance (PERF)

- [ ] **PERF-01**: Hình ảnh được lazy load — chỉ tải khi vào viewport để cải thiện tốc độ trang

### Deploy (DEPLOY)

- [ ] **DEPLOY-01**: Site sẵn sàng deploy lên static hosting (Netlify / GitHub Pages / Vercel) với favicon và file cấu hình cơ bản

## v2 Requirements (Deferred)

- Favicon phức tạp / PWA manifest — defer sau v1
- Sitemap.xml + robots.txt — defer sau deploy và có domain thật
- Facebook Pixel — defer sau khi có ngân sách quảng cáo
- Giỏ hàng riêng — out of scope, dùng Shopee
- Blog/CMS — out of scope v1

## Out of Scope

- Backend / database riêng — dùng Shopee làm kênh bán hàng
- Hệ thống tài khoản user — không cần auth
- Giỏ hàng tự build — Shopee đã có
- Blog / content management — không trong v1

## Traceability

| REQ-ID | Phase |
|--------|-------|
| PROD-01 | Phase 1 |
| PROD-02 | Phase 1 |
| CONTACT-01 | Phase 2 |
| TRACK-01 | Phase 3 |
| SEO-01 | Phase 4 |
| PERF-01 | Phase 5 |
| DEPLOY-01 | Phase 6 |
