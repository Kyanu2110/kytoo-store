# Phase 1: Sản phẩm thật + Shopee Links - Context

**Gathered:** 2026-05-17
**Status:** Ready for planning

<domain>
## Phase Boundary

Thay thế toàn bộ placeholder (gradient, chữ cái, href="#") trong `index.html` bằng:
1. Ảnh thật của 6–10 sản phẩm KYTOO (upload vào `/images/`)
2. Link Shopee thật — link listing riêng cho từng sản phẩm, link shop chung cho các CTA tổng quát

Đồng thời mở rộng UI từ 5 product slot hiện tại để chứa 6–10 sản phẩm thật.

**Không làm trong phase này:** Form liên hệ, GA, SEO, lazy loading, deploy config.

</domain>

<decisions>
## Implementation Decisions

### Ảnh sản phẩm
- **D-01:** Ảnh được đặt trong `/images/` folder, src dạng `/images/[filename]`. Không dùng external URL.
- **D-02:** Format: JPG hoặc PNG — không yêu cầu convert sang WebP.
- **D-03:** Đổi aspect ratio product cards từ `aspect-video` (16:9) sang `aspect-square` (1:1) cho phù hợp với ảnh Shopee chuẩn vuông.

### Danh sách sản phẩm
- **D-04:** 5 sản phẩm placeholder hiện tại (Jett Hoodie, Reyna Keycap, Sage Art Print, Neon Mug, Killjoy Mousepad) phải được thay hoàn toàn — đây KHÔNG phải sản phẩm thật KYTOO.
- **D-05:** Tổng số sản phẩm thật: 6–10. UI cần mở rộng để chứa thêm slot (hiện có 5).
- **D-06:** Tên, giá, danh mục, và ảnh của từng sản phẩm thật sẽ do user cung cấp khi execute (paste vào chat). Planner cần chuẩn bị cấu trúc linh hoạt để nhận input này.

### Shopee Links
- **D-07:** Shop KYTOO đã mở và có listing riêng cho từng sản phẩm.
- **D-08:** CTA tổng quát ("Xem tất cả", nút "SHOPEE" mini trong agent tabs) → trỏ đến trang shop chính của KYTOO trên Shopee.
- **D-09:** Nút từng sản phẩm ("Mua trên Shopee", "Mua ngay") → trỏ đến đúng listing riêng của sản phẩm đó.
- **D-10:** Toàn bộ Shopee URLs sẽ được user paste vào chat khi execute. Planner cần tạo cơ chế rõ ràng để Claude map URLs vào đúng slot (comment TODO hoặc data attribute).

### Xử lý thiếu ảnh
- **D-11:** Tất cả sản phẩm trong v1 đều có ảnh sẵn sàng — không cần xử lý trạng thái thiếu ảnh khi execute.
- **D-12:** Fallback cho tương lai (thêm sản phẩm mới): giữ CSS gradient Valorant làm fallback — không ẩn sản phẩm. Implement bằng `onerror` trên `<img>` tag.

### Claude's Discretion
- Cách expand UI để chứa 6–10 sản phẩm (thêm slide vào carousel, thêm tab agent, hoặc section grid mới) — Claude chọn cách phù hợp nhất với codebase hiện tại.

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Requirements & Scope
- `.planning/REQUIREMENTS.md` — PROD-01 (ảnh thật), PROD-02 (link Shopee thật) — success criteria cho phase này
- `.planning/ROADMAP.md` — Phase 1 goal, mode: mvp, 3 success criteria cụ thể

### Project Context
- `.planning/PROJECT.md` — danh sách sản phẩm placeholder hiện tại, context Shopee là kênh bán duy nhất, tech stack constraints

### Implementation Target
- `index.html` — file duy nhất cần sửa (1542 dòng). Các section liên quan:
  - `#new-products` (dòng 333–574): 3 thumb cards + featured carousel
  - `#featured` / agent tabs (dòng 689–800): 5 agent tabs với product info
  - `#collection` (dòng 801–959): collection slider
  - 7 SHOPEE LINK comment slots (①–⑦) đánh dấu sẵn trong code

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- **CSS gradient placeholders** (e.g., `background:linear-gradient(135deg,#0e1a28,#1a2a3e)`): giữ lại làm `onerror` fallback cho `<img>` tags
- **clip-tr, clip-md, clip-sm classes**: giữ nguyên trên product cards — không thay đổi shape
- **Lucide icons** (shopping-cart, shopping-bag, chevron-right): đã có, tiếp tục dùng trong product CTAs
- **`switchAgent(index, el)` JS function** (dòng ~1300+): điều khiển agent tabs — planner cần hiểu cơ chế này để mở rộng tab

### Established Patterns
- **Single-file HTML**: mọi thay đổi chỉ trong `index.html` — không tạo file JS/CSS riêng
- **Tailwind CDN classes**: không compile, chỉ dùng class có sẵn trong CDN build
- **SHOPEE LINK comments (①–⑦)**: đã có 7 slot được đánh dấu trong code — planner cần map thêm slot cho sản phẩm mới
- **`aspect-video` → `aspect-square`**: tất cả product image containers cần đổi class này

### Integration Points
- `<img>` tags mới cần `onerror` inline để fallback về gradient nếu ảnh lỗi
- Agent tabs (`switchAgent` function) cần được cập nhật data (name, price, desc, img, shopee-link) cho mỗi sản phẩm mới — kiến trúc hiện tại hardcode trong JS array

</code_context>

<specifics>
## Specific Ideas

- Ảnh Shopee thường là 1:1 (vuông) — đổi sang `aspect-square` là quyết định đúng với format thực tế
- User sẽ cung cấp product data (tên, giá, ảnh filename, Shopee link) dạng list khi execute — executor cần hỏi/nhận input này trước khi code

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope.

</deferred>

---

*Phase: 1-Sản phẩm thật + Shopee Links*
*Context gathered: 2026-05-17*
