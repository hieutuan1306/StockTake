# MAXIDI Store Stocktake – Multi Device

Web app kiểm kê cửa hàng MAXIDI, hỗ trợ nhiều điện thoại cùng tham gia một phiên kiểm kê và tổng hợp dữ liệu realtime qua Firebase Realtime Database.

## Chức năng chính

- Tạo cửa hàng và phiên kiểm kê bằng Session Code.
- Khai báo/import danh sách vị trí cần kiểm.
- Import danh mục hàng hóa.
- Nhiều điện thoại cùng tham gia một Session Code.
- Quét location, sau đó quét barcode hoặc nhập PLU và nhập số lượng.
- Tổng hợp dữ liệu kiểm kê theo SKU/location.
- Theo dõi location đã kiểm/chưa kiểm.
- Xuất Excel gồm: Summary, Detail, Location Summary, Exceptions.

## Deploy bằng GitHub Pages

1. Tạo repository mới trên GitHub.
2. Upload toàn bộ file trong package này vào **root** của repository.
3. Vào **Settings → Pages**.
4. Ở **Build and deployment**, chọn **Deploy from a branch**.
5. Chọn branch `main`, folder `/(root)` rồi **Save**.
6. Sau khi GitHub Pages publish, mở URL của website trên điện thoại/desktop.

`index.html` là file chạy chính nên không cần build framework hay cài package.

## Cấu hình nhiều thiết bị bằng Firebase

App có thể test local trên một máy mà chưa cần Firebase. Để nhiều điện thoại cùng ghi vào một phiên kiểm kê, cần Firebase Realtime Database.

### 1. Tạo Firebase project

- Tạo project trên Firebase Console.
- Thêm một **Web App**.
- Tạo **Realtime Database**.
- Lấy Firebase Web Config.

Config thường có dạng:

```json
{
  "apiKey": "...",
  "authDomain": "...",
  "databaseURL": "https://....firebasedatabase.app",
  "projectId": "...",
  "storageBucket": "...",
  "messagingSenderId": "...",
  "appId": "..."
}
```

### 2. Nhập config vào app

- Mở website.
- Vào tab **Cấu hình Sync**.
- Dán nguyên JSON Firebase Config.
- Chọn **Lưu & kết nối**.
- Trạng thái phía trên sẽ chuyển thành **Realtime connected** khi kết nối thành công.

Config hiện được lưu trong localStorage của từng trình duyệt, vì vậy mỗi điện thoại cần cấu hình Firebase một lần.

## Firebase Database Rules

Khi chỉ test nội bộ, có thể tạm dùng rule test trong thời gian ngắn. Khi đưa vào vận hành thật, nên cấu hình Firebase Authentication và Database Rules để tránh người ngoài đọc/ghi dữ liệu kiểm kê.

Không nên để database production ở chế độ public read/write lâu dài.

## Quy trình vận hành đề xuất

### Máy trưởng ca / người phụ trách

1. Mở tab **Setup**.
2. Nhập mã cửa hàng, ngày kiểm kê và Session Code.
3. Nạp danh sách Location.
4. Nạp Product Master.
5. Chọn **Tạo / mở phiên kiểm**.
6. Gửi Session Code cho các nhân viên kiểm kê.

### Điện thoại kiểm kê

1. Mở cùng URL GitHub Pages.
2. Nhập Session Code.
3. Nhập tên/MSNV người kiểm.
4. Quét/chọn Location.
5. Quét Barcode hoặc nhập PLU.
6. Nhập Qty và ghi nhận.
7. Tiếp tục SKU tiếp theo; chỉ đổi Location khi chuyển khu vực kiểm kê.

### Kết thúc kiểm kê

Trên máy quản lý, vào tab **Tổng hợp** để xem tiến độ và xuất Excel tổng hợp toàn cửa hàng.

## File trong package

- `index.html` – ứng dụng web chính.
- `README.md` – hướng dẫn deploy và cấu hình.
- `.gitignore` – file Git cơ bản.

## Phiên bản

MAXIDI Store Stocktake MultiDevice V1 – 2026-10-01
