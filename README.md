# lockday.xyz

Website tĩnh của LockDay: landing page, Privacy Policy, Terms of Use và file cấu hình app đọc khi mở.
Không có bước build — HTML/CSS thuần, deploy thẳng thư mục gốc (Cloudflare Pages hoặc GitHub Pages).

## Cấu trúc
- `index.html` — trang chủ tối giản (tên app, câu giới thiệu, 3 màn hình khoá, 4 ý chính). Cố ý không ghi giá, số lượng mẫu/widget hay giới hạn để app nâng cấp không phải sửa web.
- `privacy/index.html`, `terms/index.html` — app mở `https://lockday.xyz/privacy` và `/terms` từ Cài đặt và paywall.
- `config.json` — app đọc lúc mở (`RemoteConfig.swift`). Khoá: `shortcutURL` (link iCloud của phím tắt),
  `warning` tuỳ chọn `{ "minIOS", "maxIOS", "message_en", "message_ja", "message_ko", "message_vi" }`. Phải là JSON hợp lệ.
- `assets/css/site.css` — một file CSS; màu lấy từ `LKTheme` của app.
- `assets/img/` — icon, ảnh màn hình khoá (`lock/`, mẫu trong app với ảnh nền mẫu), `og.png` (ảnh khi chia sẻ link).
- `_headers` (Cloudflare Pages: cache + CORS cho `config.json`), `CNAME` + `.nojekyll` (GitHub Pages), `404.html`, `robots.txt`, `sitemap.xml`.

## Xem thử
```bash
python3 -m http.server 8080
```
Mở http://localhost:8080.

## Trước khi public
- Email liên hệ trên web: `datfam05@gmail.com` (chốt 2026-09-15). Đổi email thì thay trong `index.html`, `privacy/`, `terms/`, `404.html`.
- App phát hành toàn cầu: Privacy và Terms không nhắc quốc gia nào, viết chung chung đủ cho Apple duyệt.
- Privacy và Terms viết chung chung (không nêu tên gói, dịch vụ cụ thể) để không phải sửa khi app đổi tính năng hay đổi nhà cung cấp.
- Khi app lên App Store, nếu muốn có nút tải: thêm badge chính thức của Apple kèm link app vào trang chủ (một lần).

## Làm lại ảnh
Ảnh màn hình khoá và widget xuất từ repo LockDay bằng bộ test `MarketingRenderTests`
(chỉ chạy khi có `TEST_RUNNER_MARKETING_DIR=/thư/mục/ra`), rồi nén bằng `sips` (JPEG cạnh dài 1226px, widget PNG 2x).
