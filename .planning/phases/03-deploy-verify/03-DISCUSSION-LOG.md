# Phase 3: Deploy & Verify — Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-05-24
**Phase:** 3-Deploy & Verify
**Areas discussed:** Shopee links, Deploy platform, Custom domain, GitHub repo, Asset management

---

## Shopee Links

| Option | Description | Selected |
|--------|-------------|----------|
| Có, tôi sẽ cung cấp 12 links | Mỗi sản phẩm có listing riêng trên Shopee | ✓ |
| Chưa — dùng link shop chung tạm | Tất cả nút dẫn về shopee.vn/kytoo_store | |
| Một số có, một số chưa | Mix thật và shop chung | |

**User's choice:** Có 12 links thật — sẽ cung cấp khi thực thi
**Notes:** Plan cần có bước thu thập 12 URLs từ user trước khi edit file.

---

## Deploy Platform

| Option | Description | Selected |
|--------|-------------|----------|
| GitHub Pages | Miễn phí, đồng bộ git, URL github.io | ✓ |
| Netlify | Drag-drop, URL tùy chỉnh, không cần git | |

**User's choice:** GitHub Pages
**Notes:** Phù hợp vì project đã có git repo local.

---

## Custom Domain

| Option | Description | Selected |
|--------|-------------|----------|
| Không — dùng URL miễn phí | github.io hoặc netlify.app | ✓ |
| Có domain riêng | Cần cấu hình DNS | |

**User's choice:** Không có custom domain — dùng URL mặc định GitHub Pages
**Notes:** Có thể thêm sau khi site live nếu user mua domain.

---

## GitHub Repo

| Option | Description | Selected |
|--------|-------------|----------|
| Rồi, đã có remote repo | Chỉ cần push và bật Pages | |
| Chưa, cần tạo mới | Tạo repo, add remote, push lần đầu | ✓ |
| Không chắc | Cần kiểm tra git remote | |

**User's choice:** Chưa có repo — cần tạo mới
**Notes:** Plan cần hướng dẫn tạo repo trên GitHub và setup remote.

---

## Asset Management (Video & Font)

| Option | Description | Selected |
|--------|-------------|----------|
| Có — push hết | Video và font là thành phần quan trọng | ✓ |
| Chỉ font, bỏ video | Nhẹ hơn, load nhanh hơn | |

**User's choice:** Push tất cả files cần thiết cho site
**Notes:** Cần phân biệt files dùng trong site vs files nguồn lớn không dùng. Kiểm tra file size trước khi push (GitHub limit 100MB/file).

---

## Claude's Discretion

- Cách hướng dẫn tạo GitHub repo và enable Pages
- Thứ tự QA checklist
- Xử lý nếu video files vượt 100MB GitHub limit
- Tạo `.gitignore` để exclude files không cần thiết

## Deferred Ideas

- Custom domain — sau khi site live
- Google Analytics — v2
- SEO / Open Graph — v2
- GitHub LFS cho video lớn — đánh giá khi biết kích thước thực tế
