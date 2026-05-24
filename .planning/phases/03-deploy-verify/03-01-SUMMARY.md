---
phase: 03-deploy-verify
plan: 01
status: complete
completed: 2026-05-24
requirements_satisfied:
  - TECH-03
---

# Summary: Deploy KYTOO Store to GitHub Pages

## What Was Built

KYTOO Store is now live at a public HTTPS URL with all Shopee product links filled in and QA verified.

## Live URLs

- **Site:** https://kytooshop.github.io/kytoo-store/
- **GitHub repo:** https://github.com/kytooshop/kytoo-store
- **Shopee shop:** https://shopee.vn/kytoo_store

## Shopee Links Filled In

| # | Product | URL |
|---|---------|-----|
| 1 | mysterybox | https://vn.shp.ee/qGq2rsEw |
| 2 | keycapcustom | https://vn.shp.ee/zyGrtYvW |
| 3 | keycap14phim | https://vn.shp.ee/ybYx5k17 |
| 4 | tactical | https://vt.tiktok.com/ZS9YjUWDNkcH7-E9gbu/ (TikTok — not on Shopee) |
| 5 | wingman | https://vt.tiktok.com/ZS9YjUtwNKdFv-Brthv/ (TikTok — not on Shopee) |
| 6 | nhanclove | https://vn.shp.ee/Z64uAvxY |
| 7 | nuochoa | https://vn.shp.ee/KoiyftkU |
| 8 | blindbox | https://vn.shp.ee/iKH2ySrM |
| 9 | padchuot | https://vn.shp.ee/wtaWgPFC |
| 10 | miengketay | https://vn.shp.ee/3XyaGrTo |
| 11 | nhandaychuyen | https://vn.shp.ee/nHBmZdzA |
| 12 | meotreomanhinh | https://vn.shp.ee/WNdHWxex |

Navbar "Mua ngay" (desktop + mobile) → https://shopee.vn/kytoo_store

## Commits

- `feat: add assets + gitignore for GitHub Pages deploy` — .gitignore, VALORANT_Jett_Red_1_1.webp, fonts/Valorant Font.ttf
- `feat: fill all Shopee links — 12 product URLs + navbar kytoo_store` — all placeholders replaced
- `docs: phase 3 planning state + remove stale phase folder`

## QA Results

- Images: all 12 product images load, hero poster loads ✓
- Fonts: VALORANT font in hero, Be Vietnam Pro for section headings ✓
- Shopee links: navbar + all products verified ✓
- Mobile (390px): 2-col grid, hamburger, no overflow ✓
- Console: no 404 errors, no JS errors ✓

## Notes

- tactical + wingman use TikTok links (products not listed on Shopee at launch time)
- `vn.shp.ee` is Shopee's official short URL service — resolves to shopee.vn listings
- Modal "Mua trên Shopee" button href is populated at runtime by JS from PRODUCTS object
- .gitignore excludes large source MP4s (53MB Cinematic Pack), reference images, .claude/

## Self-Check: PASSED

All Phase 3 must_haves satisfied:
- [x] Site accessible at public HTTPS URL
- [x] 12 product Shopee buttons filled (10 Shopee + 2 TikTok per user decision)
- [x] Navbar "Mua ngay" → https://shopee.vn/kytoo_store
- [x] All product images load without 404
- [x] VALORANT font renders correctly on live URL
- [x] Mobile layout QA passed (390px)
- [x] TECH-03 satisfied: static deploy on GitHub Pages
