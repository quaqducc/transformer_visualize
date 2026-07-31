# Transformer — Tháp 3D

Trực quan hoá **3D tương tác** một Transformer kiểu **GPT (decoder-only)**: nhập một câu, xem forward pass **thật** (tính ngay trong trình duyệt) chảy qua embedding → các block (attention 3 head song song, MLP) → LayerNorm → Linear → Softmax, kèm số tham số từng phần và so sánh với GPT-2/GPT-3.

- **Static thuần**: chỉ một file `index.html` (HTML + CSS + JS inline). **Không backend, không build, không gọi mạng ngoài.**
- Chạy được ở bất kỳ static host nào (Vercel, Netlify, GitHub Pages, Cloudflare Pages…).

## Chạy thử ở máy

Mở thẳng `index.html` bằng trình duyệt là xong. Hoặc chạy một server tĩnh (khuyến nghị, để mọi thứ hoạt động đúng như production):

```bash
npx serve .
# hoặc
python -m http.server 8000
```

Rồi mở http://localhost:3000 (serve) hoặc http://localhost:8000.

## Deploy lên Vercel

### Cách 1 — Vercel CLI (nhanh nhất)

```bash
npm i -g vercel        # cài CLI (một lần)
cd "D:/Personal Project/Transformer Visualize"
vercel                 # đăng nhập + deploy bản preview
vercel --prod          # deploy bản production
```

Khi CLI hỏi:
- *Set up and deploy?* → **Y**
- *Which scope?* → chọn tài khoản của bạn
- *Link to existing project?* → **N** (tạo mới)
- *Framework preset?* → **Other**
- *Output/Build settings?* → để trống hết (đây là static, không cần build)

### Cách 2 — Vercel + GitHub (dễ quản lí lâu dài, khuyến nghị)

1. Đẩy repo này lên GitHub:
   ```bash
   git remote add origin https://github.com/<tên-bạn>/transformer-3d.git
   git push -u origin main
   ```
2. Vào https://vercel.com/new → **Import** repo vừa tạo.
3. Framework preset để **Other**, không cần Build Command / Output Directory → **Deploy**.
4. Từ nay mỗi lần `git push`, Vercel tự deploy lại (mỗi PR có bản preview riêng).

> Không cần `vercel.json` — Vercel tự phục vụ `index.html` ở gốc.

## Các nền tảng khác

| Nền tảng | Cách nhanh nhất |
|---|---|
| **Netlify** | Kéo–thả cả thư mục vào https://app.netlify.com/drop |
| **GitHub Pages** | Push lên GitHub → Settings → Pages → Deploy from branch `main` `/root` |
| **Cloudflare Pages** | Connect Git → build command để trống, output `/` |

## Cấu trúc & chỉnh sửa

Hiện tại toàn bộ nằm trong `index.html`:
- `<style>` — giao diện, màu, layout, hỗ trợ sáng/tối theo hệ điều hành.
- `<script>` — engine transformer (forward pass), bộ dựng cảnh 3D (tự chiếu phối cảnh, không dùng thư viện), bảng chi tiết.

Muốn dễ bảo trì hơn, có thể tách thành `index.html` + `style.css` + `app.js` — nói mình một tiếng.
