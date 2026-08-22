# legal-site — Trang pháp lý public cho TikTok Developer review

Bộ trang tĩnh để lấy 2 URL mà TikTok Developer Portal bắt buộc phải có trước khi submit app:

- **Terms of Service URL** → `terms.html`
- **Privacy Policy URL** → `privacy.html`
- **Website URL** → `index.html` (TikTok cũng hỏi ô này, và reviewer sẽ mở nó để xem app làm gì)

Không phụ thuộc framework, CDN hay build step nào — 3 file HTML + 1 file CSS, mở bằng trình duyệt là chạy.

---

## Bước 1 — Điền các chỗ còn để trống

Tìm và thay toàn bộ các token `[[...]]` trong `index.html`, `terms.html`, `privacy.html`:

| Token | Điền gì |
|---|---|
| `[[OPERATOR_NAME]]` | Tên bạn hoặc tên công ty đứng ra vận hành (VD: `Do Dao`) |
| `[[CONTACT_EMAIL]]` | Email liên hệ — **phải là email thật, reviewer có thể gửi thư tới** |
| `[[GOVERNING_LAW_COUNTRY]]` | Luật nước nào điều chỉnh (VD: `Vietnam`) |
| `[[HOSTING_LOCATION]]` | Nơi đặt dữ liệu (VD: `Vietnam`) |

Kiểm tra còn sót không:

```bash
grep -rn "\[\[" /d/Code/legal-site
```

Ngoài ra, tên **ToolHay** đang dùng xuyên suốt 3 file. Nếu trong TikTok Developer Portal bạn khai
tên app khác thì đổi lại cho **khớp tuyệt đối** — reviewer đối chiếu tên app với nội dung trang, lệch tên là một lý do bị trả về.

## Bước 2 — Đưa lên GitHub Pages (miễn phí)

Tạo repo tên đúng `<username>.github.io` (repo dạng *user site*, để file nằm ngay thư mục gốc
domain — quan trọng cho bước 3):

```bash
cd /d/Code/legal-site && git init && git add -A && git commit -m "Add legal pages for TikTok app review"
```

```bash
cd /d/Code/legal-site && git branch -M main && git remote add origin https://github.com/<username>/<username>.github.io.git && git push -u origin main
```

Vào **Settings → Pages** của repo, chọn branch `main` / thư mục `/ (root)`, lưu. Sau 1–2 phút:

- `https://<username>.github.io/terms.html`
- `https://<username>.github.io/privacy.html`
- `https://<username>.github.io/`

Mở thử ở **cửa sổ ẩn danh** để chắc chắn xem được mà không cần đăng nhập — reviewer TikTok truy cập ẩn danh.

## Bước 3 — Xác minh domain (bước bạn sẽ gặp ngay sau đó)

TikTok bắt xác minh quyền sở hữu URL trước khi cho dùng redirect URI. Cách dễ nhất với GitHub Pages
là tải file xác minh do TikTok cấp (dạng `tiktok-developers-site-verification.txt`) vào **thư mục
gốc** repo rồi push. Đó là lý do nên dùng repo `<username>.github.io` thay vì repo con — repo con
đẩy trang xuống `/<repo>/` nên không đặt được file ở gốc domain.

## Nếu sau này bạn mua tên miền riêng

Trỏ domain vào GitHub Pages (Settings → Pages → Custom domain) rồi cập nhật lại URL trong TikTok
Developer Portal. Nội dung 3 file không phải sửa gì.

---

## Lưu ý

Đây là **bản mẫu soạn theo đúng những gì hệ thống thực sự làm** (chỉ đăng video của chính bạn lên
tài khoản của chính bạn, token mã hoá trước khi lưu, không bán/chia sẻ dữ liệu), không phải tư vấn
pháp lý. Nếu sau này bạn mở dịch vụ cho người ngoài dùng thì nên nhờ luật sư rà lại.

Quan trọng hơn: **nội dung phải đúng sự thật**. Reviewer TikTok đối chiếu mô tả trong đơn với trang
này. Nếu bạn đổi phạm vi app (VD thêm đọc dữ liệu người dùng khác), phải sửa Privacy Policy cho khớp.
