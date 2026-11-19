# Công cụ gộp file Excel khối lượng

Công cụ chạy hoàn toàn trên trình duyệt: chọn từ 2 file `.xlsx` trở lên, công cụ gộp theo Tháng/Năm và biển số, cho xem trước, rồi tải về `TONG_HOP.xlsx` (kèm sheet "Báo cáo gộp"). Dữ liệu không được gửi đi đâu.

## Triển khai lên GitHub Pages

1. Tạo repository mới trên GitHub, đẩy toàn bộ thư mục này lên nhánh `main`.
2. Vào **Settings → Pages → Build and deployment → Source**, chọn **GitHub Actions**.
3. Mỗi lần push lên `main`, workflow `.github/workflows/pages.yml` sẽ chạy test rồi tự đăng. Địa chỉ có dạng `https://<tên-tài-khoản>.github.io/<tên-repo>/`.

Nếu không muốn dùng Actions: chọn **Source: Deploy from a branch**, nhánh `main`, thư mục `/ (root)`.

## Cấu trúc

| Đường dẫn | Nội dung |
|---|---|
| `index.html` | Trang chính |
| `assets/style.css` | Giao diện |
| `src/core.js` | Logic gộp (không phụ thuộc trình duyệt) |
| `src/excel-io.js` | Đọc/ghi Excel bằng ExcelJS |
| `src/ui.js` | Chọn file, xem trước, tải về |
| `tests/core.test.js` | Test cho logic gộp |

## Chạy thử trên máy

```bash
python3 -m http.server 8000   # rồi mở http://localhost:8000
node tests/core.test.js       # chạy test (cần Node 18+)
```

Có thể mở thẳng `index.html` bằng trình duyệt.

## Lưu ý

- Cần internet khi mở trang để tải thư viện ExcelJS 4.4.0 (cdnjs, dự phòng jsDelivr). Muốn chạy offline: tải `exceljs.min.js` vào `assets/` và sửa thẻ `<script>` trong `index.html`.
- Chỉ nhận `.xlsx`; file `.xls` cần lưu lại thành `.xlsx` trước.
- Tiêu đề sheet tổng hợp đang ghi tên công ty cố định trong `src/excel-io.js` (hàm `writeMergedSheet`); sửa ở đó nếu cần.
