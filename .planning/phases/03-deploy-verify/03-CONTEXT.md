# Phase 3: Deploy & Verify — Context

**Gathered:** 2026-05-24
**Status:** Ready for planning

<domain>
## Phase Boundary

Phase 3 đưa site lên URL công khai và hoàn thiện tất cả links thật:
- Tạo GitHub repo mới → push toàn bộ codebase
- Bật GitHub Pages → site live trên URL `username.github.io/repo-name`
- Điền 12 Shopee links thật vào `index.html` (do user cung cấp)
- QA toàn diện: ảnh, video, fonts, links, responsive mobile

Khi Phase 3 xong: ai nhận được URL cũng mua được hàng.

</domain>

<decisions>
## Implementation Decisions

### Deploy Platform

- **D-01:** Platform → **GitHub Pages** — miễn phí, đồng bộ với git repo, không cần service ngoài
- **D-02:** URL → mặc định GitHub Pages dạng `username.github.io/repo-name` — không cần custom domain
- **D-03:** GitHub repo → **chưa tồn tại**, cần tạo mới trên github.com, add remote, push lần đầu
- **D-04:** Branch deploy → `master` (branch hiện tại) — cấu hình GitHub Pages để serve từ `master / (root)`

### Shopee Links

- **D-05:** User sẽ cung cấp 12 URLs Shopee thật trong quá trình thực thi — plan phải có **bước thu thập links** trước khi điền (hỏi user, đợi response, rồi mới edit file)
- **D-06:** 12 `shopee: '#shopee-{product}'` placeholder trong JS object PRODUCTS → thay bằng URL thật tương ứng
- **D-07:** Navbar "Mua ngay" (`#shopee-placeholder`) → thay bằng `https://shopee.vn/kytoo_store` (shop page chung, không cần listing cụ thể)
- **D-08:** Hero CTA "Khám phá sản phẩm" → giữ nguyên `#san-pham` (scroll xuống, không Shopee)

### Asset Management

- **D-09:** Files cần push lên git (site không hoạt động nếu thiếu):
  - `index.html`
  - `fonts/Valorant Font.ttf` — font VALORANT hero heading
  - `VALORANT_Jett_Red_1_1.webp` — poster fallback hero section
  - `images/*.jpg / .png / .webp` — 12 ảnh sản phẩm + ảnh chi tiết
  - `images/hero.mp4` — nếu đây là video hero (cần verify path match với `<source src="hero.mp4">`)
  - Các `bg-*.mp4` video section backgrounds (nếu tồn tại)
- **D-10:** Files KHÔNG push (source material, không referenced trong index.html):
  - `"FREE Valorant Cinematic Pack...mp4"` — file nguồn lớn
  - `"omen darkness valorant...mp4"` — file nguồn lớn
  - `index-backup.html` — backup không dùng
  - `Valorant-mobile-leak-1-e1649777345675.jpg`, `valorant-umfrage-titel-1-01.jpg`, `valorant.webp`, `Untitled.png` — ảnh reference không dùng
- **D-11:** Kiểm tra file size trước khi push — GitHub limit 100MB/file; nếu video vượt ngưỡng → cần xem xét (Claude discretion: thông báo user, đề xuất .gitignore video lớn + CDN link thay thế nếu cần)
- **D-12:** Thêm `.gitignore` để exclude các file không cần thiết trong D-10

### Claude's Discretion

- Cách tạo GitHub repo: hướng dẫn user làm trên web hoặc dùng `gh` CLI (tùy môi trường)
- Cách enable GitHub Pages: hướng dẫn từng bước trong Settings → Pages
- Thứ tự QA checklist: ảnh → video → fonts → links → responsive → cross-browser
- Nếu video file quá lớn cho git: đề xuất phương án (LFS, CDN, skip video) và hỏi user

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Design System & Codebase
- `CLAUDE.md` — Design system đầy đủ, stack rules (single-file, no build step)
- `index.html` — File duy nhất cần modify; tất cả Shopee links nằm trong JS object `PRODUCTS` gần cuối file

### Project Context
- `.planning/PROJECT.md` — Core value, constraints, out-of-scope
- `.planning/REQUIREMENTS.md` — TECH-03: deploy tĩnh tương thích GitHub Pages / Netlify
- `.planning/STATE.md` — Trạng thái hiện tại, extra work đã làm

### Prior Phase Decisions (đọc để tránh đụng patterns)
- `.planning/phases/02-products-about-contact/02-CONTEXT.md` — D-05/D-08/D-09: Shopee links placeholder pattern, Zalo/FB links format, About section stats

### Assets (cần push lên git)
- `fonts/Valorant Font.ttf` — font hero heading (local, không CDN)
- `VALORANT_Jett_Red_1_1.webp` — hero poster fallback
- `images/` — 12 ảnh sản phẩm + ảnh chi tiết

</canonical_refs>

<code_context>
## Existing Code Insights

### Shopee Link Locations (3 điểm cần update)
1. **Navbar desktop**: `<a href="#shopee-placeholder" ...>Mua ngay</a>` (line ~193)
2. **Navbar mobile**: `<a href="#shopee-placeholder" ...>Mua ngay</a>` (line ~211)
3. **PRODUCTS JS object**: 12 entries với `shopee: '#shopee-{name}'` (lines ~494–573) — đây là nguồn cho modal "Mua trên Shopee" button

### Video References trong index.html
```
hero.mp4          → hero section background
bg-sanpham.mp4    → #san-pham section background
bg-bosuutap.mp4   → #bo-suu-tap section background
bg-vekytoo.mp4    → #ve-kytoo section background
bg-lienhe.mp4     → #lien-he section background
```
Tất cả referenced tại root level (không có prefix `images/`).

### Untracked Files cần Xử lý
- `fonts/` — cần push (site dùng)
- `images/hero.mp4` — path khác với `hero.mp4` trong HTML, cần kiểm tra path thực tế
- `VALORANT_Jett_Red_1_1.webp` — cần push
- Các MP4 lớn tên dài ở root — loại trừ khỏi git

### Established Patterns
- Zalo link: `https://zalo.me/0347470186` (đã có thật)
- Facebook link: `https://www.facebook.com/kyanu2110` (đã có thật)
- Shopee shop: `https://shopee.vn/kytoo_store` (đã dùng trong footer + contact)

</code_context>

<specifics>
## Specific Ideas

- Shopee links cần user cung cấp — plan phải prompt user nhập 12 URLs trước khi edit file (không hardcode placeholder)
- Navbar "Mua ngay" → `https://shopee.vn/kytoo_store` (không cần hỏi thêm)
- GitHub Pages deploy từ `master` branch, root directory — đơn giản nhất, không cần cấu hình phức tạp

</specifics>

<deferred>
## Deferred Ideas

- Custom domain (kytoo.gg, kytoo.vn) — user chưa có, có thể làm sau khi site live
- Google Analytics — v2 theo REQUIREMENTS.md
- SEO / Open Graph — v2 theo REQUIREMENTS.md
- Lazy loading ảnh — v2 optimization
- GitHub LFS cho video files nếu vượt 100MB limit — đánh giá khi check file size thực tế

</deferred>

---

*Phase: 3-Deploy & Verify*
*Context gathered: 2026-05-24*
