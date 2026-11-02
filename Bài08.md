

# Phần 1: Phân tích lỗ hổng và nguyên nhân

## Câu 1: Nguyên nhân hiển thị dữ liệu thuốc cũ
- Browser Cache lưu file CSS, JSON trên RAM hoặc ổ đĩa.
- Khi tải lại, trình duyệt sử dụng bản Cache cũ thay vì lấy dữ liệu mới từ Server.
- Dấu hiệu: `(from disk cache)` hoặc `(from memory cache)`.

## Câu 2: Lỗ hổng bảo mật Cookie
- JavaScript có thể đọc Cookie không có HttpOnly bằng:
  `document.cookie`
- Thiếu HttpOnly: Mã JavaScript độc hại (XSS) có thể đọc và đánh cắp Token phiên.
- Thiếu Secure: Cookie có thể bị gửi qua HTTP không mã hóa.
- Hậu quả: Hacker chiếm phiên đăng nhập, truy cập trái phép hồ sơ bệnh án.

# Phần 2: Giải pháp và thao tác DevTools

## Câu 3: Hard Reload
- Windows: `Ctrl + Shift + R`
- macOS: `Cmd + Shift + R`
- Tải lại tài nguyên, không xóa lịch sử duyệt web.

## Câu 4: Cấu hình Set-Cookie an toàn
```http
Set-Cookie: carepulse_doctor_session=TOKEN_XYZ883921983; Path=/; Max-Age=3600; HttpOnly; Secure; SameSite=Strict
```

- HttpOnly: Ngăn JavaScript đọc Cookie.
- Secure: Chỉ gửi Cookie qua HTTPS.
- SameSite=Strict: Hạn chế gửi Cookie trong yêu cầu từ trang khác.
- Max-Age=3600: Cookie hết hạn sau 1 giờ.

## Câu 5: Ba bước kiểm tra bằng DevTools
1. Mở DevTools (`F12` hoặc `Cmd + Option + I` trên Mac).
2. Vào `Application → Cookies` kiểm tra HttpOnly, Secure, SameSite.
3. Vào `Network → Disable cache`, sau đó tải lại trang để lấy dữ liệu mới.

## Kết luận
- Browser Cache: Lưu tài nguyên để tăng tốc tải trang.
- HTTP Cookies: Duy trì phiên đăng nhập.
- Giải pháp: Hard Reload, Disable Cache và cấu hình Cookie bảo mật.

