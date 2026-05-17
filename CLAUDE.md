# KYTOO.GG — Project Guide

## Project

Valorant merch store landing page cho thị trường Việt Nam. Single-file HTML static site, không có backend, bán hàng qua Shopee.

## Tech Stack

- **HTML/CSS/JS:** Single file `index.html` (1542 lines), Tailwind CSS CDN, Lucide icons, Vanilla JS
- **Fonts:** Google Fonts — Rajdhani (headings), Inter (body)
- **Colors:** `#FF4655` (vr/red), `#111111` (vdark), `#ECE8E1` (vcream), `#0F1923` (vdeep)
- **No build system** — edit `index.html` trực tiếp

## GSD Workflow

Project dùng GSD (Get Shit Done) workflow. Planning docs ở `.planning/`.

```
/gsd:discuss-phase N   — gather context trước khi plan
/gsd:plan-phase N      — tạo PLAN.md cho phase N
/gsd:execute-phase N   — thực thi plans
/gsd:verify-work N     — verify phase hoàn thành
/gsd:progress          — xem trạng thái tổng quan
```

## Conventions

- **Không thêm framework** — giữ static HTML thuần
- **Không thêm build step** — Tailwind CDN, không cần compile
- **Shopee là kênh bán duy nhất** — không build cart riêng
- **Ảnh:** Đặt trong thư mục `/images/` hoặc dùng CDN

## Sections trong index.html

| Section | ID | Dòng (approx) |
|---------|----|---------------|
| Navbar + Hero | `#hero` | 182–327 |
| Sản phẩm mới | `#new-products` | 333–574 |
| Giới thiệu | `#about` | 580–683 |
| Agent Gear tabs | `#featured` | 689–800 |
| Bộ sưu tập | `#collection` | 801–959 |
| Guides | `#guides` | 960–1031 |
| Gallery | `#gallery` | 1032–1182 |
| Liên hệ | `#contact` | 1183–1244 |
| Footer + JS | — | 1244–1542 |

## Clip-path classes

```css
.clip-lg    /* large corner cut */
.clip-md    /* medium corner cut */
.clip-sm    /* small corner cut */
.clip-tr    /* top-right corner cut */
.clip-tr-sm
.clip-bl    /* bottom-left corner cut */
```
