# KYTOO.GG — Project Guide

## What This Is

Landing page merch Valorant tại Việt Nam. Bán hàng qua Shopee — không tự build cart.

## Stack

- **Single-file**: Tất cả code trong `index.html` — không tạo file HTML/JS/CSS riêng
- **CSS**: Tailwind CSS CDN (không npm, không build step)
- **JS**: Vanilla JS trong `<script>` tag cuối file
- **Icons**: Lucide Icons CDN hoặc SVG inline

## Rules

1. **KHÔNG** tạo file mới ngoài `index.html` (trừ khi được yêu cầu rõ ràng)
2. **KHÔNG** cài npm packages, không thêm build step
3. **KHÔNG** tự build cart/payment — Shopee là kênh duy nhất
4. Mọi thay đổi UI → test responsive trên mobile trước
5. Color scheme: Valorant palette (đỏ `#FF4655`, đen `#0F1923`, trắng)

## Assets

- **Ảnh sản phẩm**: `images/` — mysterybox.jpg, blindbox.jpg, keycap14phim.jpg, keycapcustom.jpg, padchuot.jpg, nhanclove.jpg, nhandaychuyen.png, wingman.jpg, tactical.jpg, nuochoa.jpg, miengketay.jpg, meotreomanhinh.jpg
- **Hero background**: `VALORANT_Jett_Red_1_1.webp` (root)

## GSD Workflow

Dự án này dùng GSD (Get Shit Done) workflow:

```
/gsd:discuss-phase 1   — thảo luận trước khi plan
/gsd:plan-phase 1      — tạo plan chi tiết
/gsd:execute-phase 1   — thực thi phase
/gsd:verify-work 1     — verify deliverables
```

Planning files: `.planning/`
- `PROJECT.md` — project context
- `REQUIREMENTS.md` — v1 requirements với REQ-IDs
- `ROADMAP.md` — 3 phases, success criteria
- `STATE.md` — trạng thái hiện tại

## Next Step

```
/gsd:discuss-phase 1
```

Phase 1: Core Layout & Hero — HTML skeleton + hero section
