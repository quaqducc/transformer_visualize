# Giải Mã — blog kiến thức CNTT bằng hình

**Giải Mã** là một blog về Công nghệ thông tin, giải thích các khái niệm bằng **hình ảnh trực quan** và, khi có thể, bằng **demo tương tác chạy thật** trong trình duyệt.

- **Static thuần**: HTML + CSS + JS inline. **Không backend, không build, không gọi mạng ngoài.**
- Tông màu **đỏ – đen**, hỗ trợ sáng/tối (nút chuyển + theo hệ điều hành).
- Chạy được ở bất kỳ static host nào (Vercel, Netlify, GitHub Pages, Cloudflare Pages…).

## Cấu trúc

```
index.html                 ← Trang chủ blog: hero + bài nổi bật + danh sách bài (lọc theo chủ đề)
about.html                 ← Giới thiệu
style.css                  ← Khung dùng chung: tokens (đỏ–đen) + base + header/footer/nút
posts/
  transformer.html         ← Bài: "Bên trong một Transformer" (tháp 3D GPT) — self-contained
  git.html                 ← Bài: "Git: nhánh & dòng thời gian" (đồ thị commit tương tác)
README.md  ·  .gitignore
```

- **`style.css` dùng chung**: design tokens (đỏ–đen, sáng/tối) + header/footer/nút. Đổi màu thương hiệu chỉ cần sửa một nơi. Trang chủ, Giới thiệu và bài Git link tới nó; bài **Transformer để self-contained** (có bảng màu riêng đã tinh chỉnh, sinh tự động — mỗi bài tương tác là một file portable).
- Header/footer & bộ màu giống nhau trên mọi trang; nút 🌙/☀️ đổi sáng/tối (lưu bằng `localStorage`).
- Trang chủ có **lọc theo chủ đề** (AI/ML · Cơ bản · Thuật toán · Hệ thống · Web) bằng JS thuần.

### Thêm một bài viết mới
1. Tạo file `posts/<tên>.html` (một trang self-contained, có nút `← Giải Mã` về `../index.html`).
2. Ở `index.html`, copy một thẻ `<a class="card" data-cat="...">` trong `#cards`, sửa icon/tiêu đề/mô tả/link và `data-cat` (để lọc đúng chủ đề). Bỏ class `soon` khi bài đã sẵn sàng.

## Chạy thử ở máy

```bash
npx serve .
# hoặc
python -m http.server 8000
```
Mở http://localhost:3000 (serve) hoặc http://localhost:8000. (Nên chạy qua server để đường dẫn giữa các trang đúng như production.)

## Deploy lên Vercel

- **GitHub → Vercel (khuyến nghị):** repo đã ở GitHub → https://vercel.com/new → **Import** → Framework preset **Other**, để trống Build/Output → **Deploy**. Mỗi `git push` sau đó tự deploy lại.
- **CLI:** `npm i -g vercel` rồi `vercel` (preview) / `vercel --prod`.

> Không cần `vercel.json` — Vercel tự phục vụ `index.html` ở gốc và các file trong `posts/`.

## Thương hiệu

- Tên **Giải Mã** và logo (3 thanh xếp lớp, thanh đỏ trên cùng — “bóc tách kiến thức thành lớp rõ ràng”) là inline SVG + favicon data-URI, đổi được ngay trong `index.html` / `about.html`.
- Muốn tách `style.css` / `app.js`, đổi tên brand, hay thêm bài mới — cứ nói.
