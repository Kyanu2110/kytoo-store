# Phase 2: Products, About & Contact — Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-05-22
**Phase:** 02-products-about-contact
**Areas discussed:** Product data, Card → Modal UX, Bộ sưu tập section

---

## Product data

| Option | Description | Selected |
|--------|-------------|----------|
| Có, mình sẽ cung cấp | User type tên + giá cho từng ảnh ngay | ✓ |
| Chưa có — dùng placeholder | Claude đặt tên tạm dựa theo tên file ảnh | |
| Có 1 phần — mix thật + placeholder | | |

**User's choice:** Cung cấp data thực cho tất cả 12 sản phẩm (xem bảng trong CONTEXT.md D-07).

**Notes:**
- `nhanclove.jpg` bị bỏ sót lần đầu — user bổ sung: "Bộ 3 Nhẫn Clove Tuỳ Chỉnh Được Kích Thước, Trang Sức Valorant Đeo Tay, Độc Đáo Cho Duo Của Bạn" / 79.000₫
- `tactical.jpg` và `wingman.jpg` tên bị lộn: user confirm đổi lại — tactical.jpg = Tactical Bear (279.000₫), wingman.jpg = Wingman (152.100₫)
- `nhandaychuyen.png` giá: 37.000₫ – 44.100₫ (user ghi ngược 44.100₫ – 37.000₫, mình sửa thành min → max)
- Tên đầy đủ trên card (Shopee-style) — user chọn không rút gọn
- Order: giá giảm dần (mysterybox đầu, meotreomanhinh cuối)

---

## Card → Modal UX

| Option | Description | Selected |
|--------|-------------|----------|
| Chỉ click card mở modal — Shopee button nằm trong modal | Card gọn hơn, user xem sản phẩm trước khi đi Shopee | ✓ |
| Card có cả 2: click ảnh mở modal, click nút đi Shopee luôn | Như Shopee layout — 2 action rõ ràng trên card | |

**Modal content (multiSelect):** Ảnh lớn ✓, Tên + giá đầy đủ ✓, Mô tả ngắn ✓, Nút "Mua trên Shopee" ✓

**Grid columns:** 4 cột desktop (user chọn, 12 sản phẩm = 3 hàng đều)

**Notes:**
- Claude discretion: close modal bằng X button + click outside + Escape key (standard UX)
- Mô tả ngắn: Claude draft 1-2 câu dựa theo tên sản phẩm
- Shopee button link placeholder Phase 3

---

## Bộ sưu tập section

| Option | Description | Selected |
|--------|-------------|----------|
| Gallery ảnh sản phẩm (masonry/grid) | Hiển thị ảnh đẹp kiểu look-book — không có tên/giá, chỉ visual | ✓ |
| Featured subset — chọn 4-6 sản phẩm nổi bật | Curated collection riêng | |
| Bỏ section này | Để trống Phase 3 quyết định | |
| Dùng cho ảnh lifestyle/in-use | Ảnh đồ đang dùng thực tế | |

**Ảnh gallery:** Dùng lại 12 ảnh sản phẩm sẵn có (không cần ảnh thêm)

**Notes:**
- Phân biệt với section Sản Phẩm: gallery KHÔNG có tên/giá/button
- Layout masonry hoặc CSS grid bất đối xứng (per CLAUDE.md Gallery Grid pattern)
- Thuần visual — phong cách lookbook

---

## Claude's Discretion

- About section copy: Claude draft dựa vào project context (Valorant-themed VN merch)
- Contact links: Zalo + Facebook với placeholder links — user điền thật Phase 3
- Modal animation: CSS transition nhẹ
- Card hover: scale + border-red per CLAUDE.md

## Deferred Ideas

- Actual Shopee product URLs → Phase 3
- Actual Zalo/Facebook URLs → Phase 3
- Real social proof numbers → Phase 3
