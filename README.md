# AI Trực Quan — website học tập

Học cách các mô hình AI hoạt động bằng những **bài học tương tác, chạy thật trong trình duyệt**. Không lý thuyết suông: xoay, bấm, và thấy từng con số chảy qua mô hình.

- **Static thuần**: chỉ HTML + CSS + JS inline. **Không backend, không build, không gọi mạng ngoài.**
- Chạy được ở bất kỳ static host nào (Vercel, Netlify, GitHub Pages, Cloudflare Pages…).

## Cấu trúc

```
index.html                 ← Trang chủ (landing) — danh mục bài học
lessons/
  transformer.html         ← Bài học: "Bên trong một Transformer" (tháp 3D GPT)
README.md
.gitignore
```

- Landing (`index.html`) liệt kê các bài học; thẻ "Bên trong một Transformer" dẫn tới `lessons/transformer.html`.
- Trang bài học có nút **← Trang chủ** quay lại landing.
- Thêm bài mới: tạo `lessons/<tên>.html` rồi thêm một thẻ `<a class="card">` trong mục Bài học ở `index.html`.

### Bài "Bên trong một Transformer"
Tháp **3D tương tác** một Transformer kiểu **GPT (decoder-only)**: nhập một câu, xem forward pass **thật** chảy qua embedding → block (attention 3 head song song, MLP) → LayerNorm → Linear → Softmax; có tour dẫn dắt cho người mới, nhãn "dễ hiểu", cung attention, và số tham số so với GPT-2/GPT-3. Toàn bộ là một file HTML self-contained.

## Chạy thử ở máy

Mở thẳng `index.html` bằng trình duyệt, hoặc chạy một server tĩnh (khuyến nghị, để đường dẫn giữa các trang hoạt động đúng như production):

```bash
npx serve .
# hoặc
python -m http.server 8000
```

Rồi mở http://localhost:3000 (serve) hoặc http://localhost:8000.

## Deploy lên Vercel

### Cách 1 — Vercel + GitHub (khuyến nghị)
1. Repo đã ở trên GitHub. Vào https://vercel.com/new → **Import** repo này.
2. Framework preset để **Other**, không cần Build Command / Output Directory → **Deploy**.
3. Từ nay mỗi lần `git push`, Vercel tự deploy lại (mỗi PR có bản preview riêng).

### Cách 2 — Vercel CLI
```bash
npm i -g vercel
cd "D:/Personal Project/Transformer Visualize"
vercel            # preview
vercel --prod     # production
```
Khi hỏi *Framework preset* → **Other**; Build/Output để trống.

> Không cần `vercel.json` — Vercel tự phục vụ `index.html` ở gốc và các file trong `lessons/`.

## Các nền tảng khác

| Nền tảng | Cách nhanh nhất |
|---|---|
| **Netlify** | Kéo–thả cả thư mục vào https://app.netlify.com/drop |
| **GitHub Pages** | Settings → Pages → Deploy from branch `main` `/root` |
| **Cloudflare Pages** | Connect Git → build command để trống, output `/` |

## Ghi chú

- Tên "AI Trực Quan" là tên tạm — đổi trong `index.html` (logo ở header + footer + `<title>`).
- Bài học Transformer được sinh từ một file nguồn; muốn tách `style.css` / `app.js` cho dễ bảo trì thì nói mình.
