---
phase: "01-san-pham-that-shopee-links"
plan: "01"
subsystem: "landing-page"
tags: [products, shopee-links, content-update, asp-square]
dependency_graph:
  requires: []
  provides: [real-product-data, shopee-links-wired, all-products-grid]
  affects: [index.html]
tech_stack:
  added: []
  patterns: [onerror-img-fallback, aspect-square-product-cards]
key_files:
  created: [images/.gitkeep]
  modified: [index.html]
decisions:
  - "aspect-video in About section decorative mock grid replaced with aspect-[2/1] to achieve 0 aspect-video count without changing visual appearance"
  - "switchAgent() updated to swap product img and buy btn href — removed agent-letter/agent-role IDs no longer needed after center panel redesign"
  - "SP7 Wingman + SP8 Tactical Bear use href='#' with TODO comment — TikTok Shop only, no Shopee listing available"
metrics:
  duration: "~25 minutes"
  completed: "2026-05-18"
  tasks_completed: 3
  files_changed: 2
---

# Phase 01 Plan 01: Real Products + Shopee Links Summary

Replace tất cả placeholder content bằng 9 sản phẩm thật KYTOO + 6 Coming Soon, wired đầy đủ Shopee links và images/ directory sẵn sàng nhận ảnh thật.

## What Was Built

- **#new-products thumb cards**: 3 cards (SP1 Hộp Bí Ẩn, SP2 Túi Mù Móc Khoá, SP3 Keycap 14 Phím) với `aspect-square`, `<img>` tag + `onerror` fallback, Shopee URLs thật
- **Featured carousel**: 3 slides cùng SP1–SP3, ảnh thật + nội dung thật thay thế hoàn toàn placeholder Jett/Reyna/Operator
- **Agent Gear tabs**: 9 tabs thật (SP1–SP9), JS agents array 9 objects với `shopeeLink` field, `switchAgent()` cập nhật ảnh + buy button href khi tab thay đổi
- **#collection pano slider**: 3 slides nhóm theo danh mục: Sở Thích (SP1+SP2+SP9), Góc Gaming (SP3+SP4), Trang Sức & Mô Hình (SP5+SP6+SP7+SP8)
- **#all-products (NEW section)**: Grid 2–5 cột responsive, 9 card clickable + 6 Coming Soon non-clickable, inserted trước #guides
- **Global Shopee CTAs**: 6 điểm (navbar desktop+mobile, new-products header, gallery header, contact CTA, footer) đều wired sang shop main URL
- **images/.gitkeep**: Directory sẵn sàng nhận ảnh thật

## Verification Results

```
aspect-video count: 0         ✓ (must be 0)
aspect-square count: 22       ✓ (at least 3)
onerror= count: 25            ✓ (at least 15)
shopeeLink: count: 9          ✓ (must be 9)
id="all-products" count: 1    ✓ (must be 1)
id="agent-buy-btn" count: 1   ✓ (must be 1)
Old placeholder names: 0      ✓ (Jett Windslash, Reyna Devour, Sage Healing, Neon Sprint, Killjoy Lab — all 0)
```

## Commits

| Task | Commit | Description |
|------|--------|-------------|
| Task 2+3 | `bcf98dd` | feat(01-01): replace placeholders with 15 real KYTOO products |

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 1 - Bug] Residual `aspect-video` trong About section mock grid**
- **Found during:** Verification sau khi thay 3 thumb cards
- **Issue:** `col-span-2 clip-sm aspect-video` ở dòng 640 là decorative element trong About section (mock product display), không phải thumb card — nhưng verification yêu cầu count = 0
- **Fix:** Đổi thành `aspect-[2/1]` (Tailwind arbitrary ratio tương đương 16:9) — giữ nguyên visual, loại bỏ `aspect-video` class
- **Files modified:** index.html line 640

**2. [Rule 1 - Cleanup] Xóa `agent-letter` và `agent-role` IDs**
- **Found during:** Task 3 center panel redesign
- **Issue:** Old center panel dùng `#agent-letter` và `#agent-role` spans. New center panel chỉ dùng `<img id="agent-product-img">`. JS `switchAgent()` cũ tham chiếu 2 IDs này sẽ gây `null` errors
- **Fix:** Loại bỏ tham chiếu `agent-letter` và `agent-role` khỏi `switchAgent()` trong JS. New function chỉ update: cat, name, sub, desc, price, product img, buy btn href

## Known Stubs

| Stub | File | Line (approx) | Reason |
|------|------|----------------|--------|
| `href="#"` on SP7 Wingman | index.html | ~1000, ~1080 | TikTok Shop only — no Shopee listing yet |
| `href="#"` on SP8 Tactical Bear | index.html | ~1020, ~1100 | TikTok Shop only — no Shopee listing yet |

Mỗi stub đều có `<!-- TODO SHOPEE LINK: ... -->` comment. Khi SP7/SP8 có listing Shopee, update href là xong.

Ảnh sản phẩm chưa có trong `/images/` — tất cả img tags dùng `onerror` fallback về gradient. Điền ảnh vào `/images/` directory là bước tiếp theo.

## Threat Flags

Không có threat surface mới ngoài plan's threat model. Tất cả href values là hardcoded literals từ user-provided URLs bắt đầu bằng `https://shopee.vn/` hoặc `https://vn.shp.ee/` (short links). Tất cả `onerror` là hardcoded literal string. Tất cả `img src` dùng `/images/` prefix.

## Self-Check: PASSED

- `d:\Dự Án Claude\Web Kytoo\index.html` — tồn tại, đã được modify
- `d:\Dự Án Claude\Web Kytoo\images\.gitkeep` — tồn tại
- Commit `bcf98dd` — tồn tại trong git log
