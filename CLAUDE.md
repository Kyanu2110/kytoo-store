# KYTOO Store — Project Guide

## What This Is

Website merch store cho KYTOO — bán sản phẩm Valorant-themed tại Việt Nam. Bán hàng qua Shopee — không tự build cart. Design style theo Valorant official site: dark gaming aesthetic, angular, high-contrast.

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
5. Giữ đúng design system bên dưới — không tự ý thêm border-radius, shadow lạ, màu ngoài palette

## Design System

### Color Palette

```
--color-bg:        #0F1923   /* nền chính — đen xanh đậm */
--color-bg-alt:    #1a2634   /* nền card, section xen kẽ */
--color-red:       #FF4655   /* accent chính — đỏ Valorant */
--color-red-dark:  #BD3944   /* hover state cho red */
--color-cream:     #ECE8E1   /* text chính trên nền tối */
--color-white:     #FFFFFF   /* text nhấn, icon */
--color-gray:      #768079   /* text phụ, caption */
--color-border:    #2a3f52   /* viền card, divider */
```

### Typography

- **Display / Hero headings**: Uppercase, bold (font-weight 800-900), letter-spacing rộng (`tracking-widest`)
- **Section headings**: Bold, có thể mix tiếng Việt — dùng `text-3xl` đến `text-5xl`
- **Body text**: Regular weight, màu `#ECE8E1`, line-height thoáng (`leading-relaxed`)
- **Labels / badges**: Uppercase small caps, `text-xs tracking-widest text-red`
- **Font**: System sans-serif hoặc Google Fonts `Inter` / `Barlow Condensed` nếu cần display

### Layout Patterns

**Navbar:**
- Fixed top, background `#0F1923` với subtle bottom border
- Logo căn giữa (hoặc trái), nav links trải đều, CTA button đỏ bên phải
- Chiều cao `h-16`

**Hero Section:**
- Full viewport height (`min-h-screen`)
- Background image với overlay `bg-gradient-to-t from-[#0F1923] via-transparent`
- Character art/ảnh chính — absolute positioned, bottom-aligned
- Text overlay: heading lớn uppercase, subtitle nhỏ, CTA button

**Cards (sản phẩm):**
- Background `#1a2634`, NO border-radius (`rounded-none`)
- Thin border `1px solid #2a3f52`
- Image chiếm 60-70% card height
- Text khu vực: padding nhỏ, tên sản phẩm cream, giá red
- Hover: scale nhẹ + border đổi sang red

**Section alternating:**
- Odd sections: nền `#0F1923`
- Even sections hoặc highlight strip: nền `#FF4655` (đỏ)
- Section headings có small red divider line phía trước

**Red accent strip:**
- Dùng cho featured section / highlight — full-width background `#FF4655`
- Text trắng, contrast cao

**Carousel / Slider:**
- Số chỉ thị kiểu `01`, `02` — angular, không dùng dot indicators
- Arrow buttons minimal, dạng `<` `>` outline

**Gallery Grid:**
- Bất đối xứng (masonry hoặc CSS grid với `grid-column: span 2` cho ảnh featured)
- Gap nhỏ `gap-1` hoặc `gap-2`
- Ảnh fill full cell, object-cover

### UI Elements

**Buttons:**
```
Primary:   bg-[#FF4655] text-white uppercase tracking-widest px-8 py-3 — NO border-radius
Secondary: border border-[#ECE8E1] text-[#ECE8E1] — NO border-radius, hover: bg đỏ
```

**Dividers / Accents:**
- Horizontal line: `border-t border-[#2a3f52]`
- Red accent line trước heading: `w-8 h-0.5 bg-[#FF4655] inline-block mr-2`
- Small Valorant-style diamond/triangle decorators — SVG inline

**Image treatment:**
- Ảnh sản phẩm: object-cover, aspect-ratio cố định
- Ảnh character/art: có thể bleed ngoài container (negative margin)
- Overlay tối trên ảnh hero: `bg-gradient-to-r from-[#0F1923]/90`

### Spacing Rhythm

- Section padding: `py-20` (desktop), `py-12` (mobile)
- Container max-width: `max-w-7xl mx-auto px-4`
- Card gap: `gap-4` desktop, `gap-3` mobile

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
