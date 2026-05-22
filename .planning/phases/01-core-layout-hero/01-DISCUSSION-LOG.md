# Phase 1: Core Layout & Hero — Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-05-22
**Phase:** 1-Core Layout & Hero
**Areas discussed:** Navbar structure, Hero text & layout, Font / Typography, Section scaffold

---

## Navbar Structure

| Option | Description | Selected |
|--------|-------------|----------|
| Logo bên trái | Logo trái, nav links giữa, CTA phải — layout phổ biến | |
| Logo căn giữa | Logo giữa, nav links hai bên — giống reference image (Valorant official site) | ✓ |

**User's choice:** Căn giữa

| Option | Description | Selected |
|--------|-------------|----------|
| Sản phẩm • Về chúng tôi • Liên hệ | 3 mục đơn giản | |
| Sản phẩm • Bộ sưu tập • Về KYTOO • Liên hệ | 4 mục đầy đủ hơn | ✓ |

**User's choice:** 4 nav links: Sản phẩm, Bộ sưu tập, Về KYTOO, Liên hệ

| Option | Description | Selected |
|--------|-------------|----------|
| "Mua ngay" → Shopee | Link thẳng đến Shopee shop, nền đỏ | ✓ |
| Không có CTA trên navbar | Chỉ nav links, CTA chính trong hero | |

| Option | Description | Selected |
|--------|-------------|----------|
| Hamburger menu | Icon ☰ mở drawer trượt xuống | ✓ |
| Ẩn hết, chỉ giữ logo | Mobile chỉ logo | |

**Notes:** User muốn giống reference image — centered logo là yếu tố nhận diện quan trọng.

---

## Hero Text & Layout

| Option | Description | Selected |
|--------|-------------|----------|
| "KYTOO" rất lớn, uppercase | Tựa được chữ brand to — giống cách VALORANT hiển thị trên hero | ✓ |
| "KYTOO STORE" + tagline | Brand name + 1 dòng mô tả nhỏ hơn | |
| Tagline là nội dung chính | Tagline nổi bật, brand name nhỏ hơn | |

| Option | Description | Selected |
|--------|-------------|----------|
| "Merch Valorant chính hãng tại Việt Nam" | Rõ ý nghĩa, định vị thương hiệu | |
| "Trang phục chiến binh. Phong cách của bạn." | Tone gamey | |
| Tôi sẽ cung cấp tagline riêng | User điền tagline thực tế sau | ✓ |

**Notes:** Tagline sẽ được bổ sung khi thấy layout thực tế.

| Option | Description | Selected |
|--------|-------------|----------|
| Căn giữa | KYTOO + tagline + CTA căn giữa hero fullscreen | ✓ |
| Căn trái | Text trái, nhường phải cho nhân vật | |

| Option | Description | Selected |
|--------|-------------|----------|
| "Mua ngay" → Shopee | Primary CTA đỏ, link đến Shopee | |
| "Khám phá sản phẩm" scroll xuống | Scroll đến section sản phẩm, không thoát trang | ✓ |

**Notes:** User muốn giữ visitor trên trang — scroll xuống sản phẩm thay vì thoát sang Shopee ngay.

---

## Font / Typography

| Option | Description | Selected |
|--------|-------------|----------|
| Rajdhani Bold | Google Font, condensed, military feel, gần Valorant aesthetic | ✓ |
| Barlow Condensed ExtraBold | Rất condensed, dày và bold | |
| Bebas Neue | All-caps chuyên biệt, game-style | |

**User's choice:** Rajdhani Bold

| Option | Description | Selected |
|--------|-------------|----------|
| Inter | Google Font, sạch, dễ đọc, Tailwind UI default | ✓ |
| Rajdhani (cùng font display) | 1 font duy nhất | |
| System sans-serif | Không tải font — nhanh nhưng kém thương hiệu | |

**User's choice:** Inter

---

## Section Scaffold

| Option | Description | Selected |
|--------|-------------|----------|
| Có — đặt đưᨋc sử của Phase 2 | Thêm section#san-pham, #ve-kytoo, #lien-he làm empty placeholder | ✓ |
| Không — chỉ hero + nav | Giữ Phase 1 gọn | |

| Option | Description | Selected |
|--------|-------------|----------|
| Footer đơn giản | Copyright + tên thương hiệu, nền tối — Phase 2 thêm Zalo/FB | ✓ |
| Không footer ở Phase 1 | Phase 2 build footer hoàn chỉnh | |

---

## Claude's Discretion

- Scroll behavior cho hamburger menu (CSS transition vs JS toggle)
- Exact min-height cho empty section placeholders
- Scroll offset compensation cho sticky navbar

## Deferred Ideas

None — discussion stayed within phase scope.
