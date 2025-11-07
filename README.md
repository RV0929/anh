# LaTeX → GitHub (public)

Repo mẫu để public file PDF và (tuỳ chọn) LaTeX.

## Cấu trúc
```
/docs
  ├─ index.html   # Trang đơn giản liên kết tới PDF
  └─ ve.pdf       # PDF (đã đổi tên ASCII để tránh lỗi mã hoá)
```

## Cách dùng
1) Tạo repo mới trên GitHub (Public), ví dụ: `my-latex-paper`.
2) Trên máy, chạy:
```bash
git init
git add .
git commit -m "init: publish PDF"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```
3) Bật **Settings → Pages → Build and deployment**
   - Source: *Deploy from a branch*
   - Branch: `main` và thư mục `/docs`
4) Xem PDF tại: `https://<username>.github.io/<repo-name>/ve.pdf`

> Lưu ý: Nếu bạn muốn GitHub tự biên dịch LaTeX thành PDF (GitHub Actions), thêm file `.tex` và workflow `latex.yml` sau:
```yaml
name: Build LaTeX PDF
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: xu-cheng/latex-action@v3
        with:
          root_file: main.tex   # đổi đúng tên file .tex chính của bạn
```
Khi đó PDF build xong sẽ xuất hiện trong artifacts (tab *Actions*) hoặc bạn có thể commit file PDF vào `/docs` để public.
