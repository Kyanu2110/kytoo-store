# Phase 1: Sản phẩm thật + Shopee Links - Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-05-17
**Phase:** 1-Sản phẩm thật + Shopee Links
**Areas discussed:** Ảnh sản phẩm — nguồn ảnh, Danh sách sản phẩm, Shopee links, Xử lý thiếu ảnh

---

## Ảnh sản phẩm — Nguồn ảnh

| Option | Description | Selected |
|--------|-------------|----------|
| Có ảnh, sẽ upload vào /images/ | Claude sẽ viết `<img src="/images/...">` — bạn upload file sau | ✓ |
| Dùng link ảnh từ Shopee/CDN | Paste URL như https://cf.shopee.vn/... vào img src | |
| Chưa có ảnh — làm slot trước | Claude đặt img tag với src rỗng / placeholder URL để sau này bạn tự điền | |

**User's choice:** Có ảnh, sẽ upload vào /images/
**Notes:** —

---

| Option | Description | Selected |
|--------|-------------|----------|
| JPG/PNG — bất kỳ kích thước | Claude viết img tag, bạn tự optimize sau | ✓ |
| WebP — đã optimize | Dùng WebP cho nhẹ hơn | |
| Bạn quyết định — Claude chọn format phù hợp nhất | JPG cho ảnh thông thường, PNG nếu cần nền trong suốt | |

**User's choice:** JPG/PNG — bất kỳ kích thước
**Notes:** —

---

| Option | Description | Selected |
|--------|-------------|----------|
| Giữ 16:9 — crop theo container | Giữ yên CSS hiện tại, ảnh sẽ có object-fit:cover | |
| 1:1 — ảnh vuông (phổ biến Shopee) | Đổi aspect ratio thành 1:1, phù hợp với ảnh Shopee của mình | ✓ |

**User's choice:** 1:1 — ảnh vuông (phổ biến Shopee)
**Notes:** Ảnh Shopee thường ở định dạng 1:1, đây là quyết định thực tế.

---

## Danh sách sản phẩm

| Option | Description | Selected |
|--------|-------------|----------|
| Đúng — giữ nguyên danh sách và giá | Chỉ cần chèn ảnh và link Shopee vào | |
| Cần cập nhật — tên/giá không khớp Shopee | Bạn sẽ cung cấp tên/giá thật để sửa | |
| Sản phẩm khác hoàn toàn — cần thả mới | UI có 5 slot, bạn sẽ điền sản phẩm thật | ✓ |

**User's choice:** Sản phẩm khác hoàn toàn — cần thả mới
**Notes:** 5 sản phẩm placeholder hiện tại không phải sản phẩm thật KYTOO.

---

| Option | Description | Selected |
|--------|-------------|----------|
| 1–4 sản phẩm — ít nhưng tập trung | UI hiện có 3 thumb card + 1 featured. Phù hợp với ít sản phẩm thật | |
| 5 sản phẩm — giữ nguyên 5 slot hiện tại | Mỗi agent tab (Jett, Reyna, Sage, Neon, Killjoy) = 1 sản phẩm | |
| Trên 5 — cần thêm slot mới | Phải mở rộng UI để chứa thêm | ✓ |

**User's choice:** Trên 5 — cần thêm slot mới
**Notes:** —

---

| Option | Description | Selected |
|--------|-------------|----------|
| 6–10 sản phẩm — vẫn quản lý được | Có thể thêm slide vào carousel, hoặc mở rộng agent tabs | ✓ |
| 11–20 sản phẩm — cần layout khác | Có thể cần section grid riêng hoặc pagination | |
| Bạn sẽ nói chính xác số lượng + danh sách trong bước execute | Claude tạo cấu trúc mở rộng được, bạn điền chi tiết sau | |

**User's choice:** 6–10 sản phẩm — vẫn quản lý được
**Notes:** Tên, giá, ảnh, link Shopee sẽ được cung cấp khi execute.

---

## Shopee Links

| Option | Description | Selected |
|--------|-------------|----------|
| Shop đã mở, có listing riêng cho từng sản phẩm | Có thể link đến listing cụ thể cho mỗi nút Mua ngay | ✓ |
| Shop đã mở nhưng chưa có listing riêng | Tạm link vào shop page — https://shopee.vn/[shop-name] | |
| Shop chưa mở — tạm bỏ qua | Link tạm shopee.vn, sau này thay khi shop mở | |

**User's choice:** Shop đã mở, có listing riêng cho từng sản phẩm
**Notes:** —

---

| Option | Description | Selected |
|--------|-------------|----------|
| Trang shop chính (shopee.vn/[shop]) | Nút chung → shop, nút sản phẩm → listing riêng | ✓ |
| Trang sản phẩm nổi bật nhất | Dẫn vào 1 listing phổ biến nhất | |
| Bạn quyết định — sẽ cung cấp links khi execute | Claude chuẩn bị cấu trúc, bạn điền URLs khi execute | |

**User's choice:** Trang shop chính (shopee.vn/[shop])
**Notes:** CTA tổng quát → shop, từng sản phẩm → listing riêng của sản phẩm đó.

---

| Option | Description | Selected |
|--------|-------------|----------|
| Paste vào chat khi execute — Claude điền vào code | Dán danh sách links và Claude map vào đúng sản phẩm | ✓ |
| Tự sửa trong index.html sau khi Claude tạo slot | Claude tạo comment TODO rõ ràng, bạn tự tìm và thay | |
| Tạo file dữ liệu riêng (products.json) — code đọc từ đó | Tách dữ liệu ra ngoài HTML — dễ cập nhật sau này | |

**User's choice:** Paste vào chat khi execute — Claude điền vào code
**Notes:** —

---

## Xử lý thiếu ảnh

| Option | Description | Selected |
|--------|-------------|----------|
| Có ảnh cho tất cả sản phẩm ngay | Claude chỉ cần chèn img tag và src | ✓ |
| Có ảnh cho một số, số còn lại chưa có | Cần quyết định xử lý sản phẩm chưa có ảnh như thế nào | |

**User's choice:** Có ảnh cho tất cả sản phẩm ngay
**Notes:** —

---

| Option | Description | Selected |
|--------|-------------|----------|
| Giữ gradient màu — Valorant aesthetic vẫn đẹp | Gradient hiện tại có vẻ rất OK như fallback | ✓ |
| Ẩn sản phẩm cho đến khi có ảnh | Không hiển thị slot rỗng trên production | |
| Bạn quyết định — Claude dùng gradient làm fallback | Dùng onerror fallback — nếu img lỗi thì hiển gradient | |

**User's choice:** Giữ gradient màu — Valorant aesthetic vẫn đẹp
**Notes:** Áp dụng qua onerror inline trên img tag.

---

## Claude's Discretion

- **Cách mở rộng UI** cho 6–10 sản phẩm: thêm slide vào carousel, thêm agent tabs, hoặc section grid mới — Claude chọn cách phù hợp nhất với codebase hiện tại.

## Deferred Ideas

None — discussion stayed within phase scope.
