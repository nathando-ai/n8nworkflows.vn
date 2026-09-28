---
title: "🚀 Tự động hóa hệ thống bán vé sự kiện: Tạo mã QR, gửi Gmail và Check-in với Google Sheets"
description: "Xây dựng backend quản lý vé sự kiện toàn diện: đăng ký qua webhook, tự động tạo mã QR, gửi email qua Gmail và quét vé check-in tại cổng hoàn toàn tự động."
slug: "tu-dong-hoa-he-thong-ban-ve-su-kien-n8n"
tags: [n8n, automation, google-sheets, gmail, qr-code, event-management]
keywords: [n8n workflow, tạo vé sự kiện tự động, mã qr n8n, google sheets n8n, gmail automation, check in vé sự kiện]
---

# 🚀 Tự động hóa hệ thống bán vé sự kiện: Tạo mã QR, gửi Gmail và Check-in

Việc quản lý vé sự kiện thủ công như nhập liệu Excel, tự thiết kế mã QR, gửi email hàng loạt cho từng khách tham dự hay kiểm tra vé bằng tay ở cổng thường rất tốn thời gian, dễ sai sót và gây ấn tượng thiếu chuyên nghiệp. 

Workflow n8n này sẽ giúp các sếp xây dựng một **Hệ thống Backend quản lý vé sự kiện tự động 100% không cần code**: từ khâu tiếp nhận đăng ký, tự động sinh mã QR độc nhất, gửi email vé qua Gmail, đến hệ thống quét mã QR check-in tại cổng sự kiện, tất cả đều được đồng bộ mượt mà với Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Khách đăng ký xong là hệ thống tự động xử lý, không cần can thiệp thủ công.
- **Tạo mã QR thông minh**: Tự sinh mã QR độc nhất cho từng vé (hỗ trợ mua nhiều vé cùng lúc) và gửi thẳng vào email khách hàng.
- **Check-in siêu tốc**: Cung cấp sẵn API endpoint để tích hợp máy quét hoặc app quét vé tại cổng, chống vé giả và chống check-in 2 lần.
- **Đồng bộ thời gian thực**: Mọi dữ liệu đăng ký và trạng thái check-in đều được cập nhật chính xác lên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã sẵn sàng chạy (Self-hosted hoặc Cloud).
- **Google Sheets Credentials**: Tài khoản Google OAuth2 để đọc/ghi dữ liệu bảng tính.
- **Gmail Credentials**: Tài khoản Gmail OAuth2 để gửi email chứa mã QR cho khách.
- **Cấu trúc Google Sheet**: Chuẩn bị sẵn 1 Google Sheet gồm 2 tab:
  - Tab 1: `Register` (Lưu thông tin người đăng ký)
  - Tab 2: `Tickets` (Lưu thông tin từng vé chi tiết)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 27 nodes chia thành các luồng chính sau:

- **Luồng Đăng ký (`REGISTER` - Webhook):**
  - Node `REGISTER` lắng nghe POST request tại đường dẫn `/v1/register`.
  - Các node `Validate Input`, `Email exist?`, `Store Data` sẽ kiểm tra dữ liệu đầu vào và lưu thông tin đăng ký mới vào tab `Register` trên Google Sheets.
  - Các node `Tiket Booked`, `Validation Error`, `Already Registered` trả về phản hồi JSON cho khách hàng.

- **Luồng Sinh vé tự động (Chạy định kỳ qua `START` - Schedule Trigger):**
  - Node `START` chạy mỗi 1 phút để quét các đơn đã thanh toán nhưng chưa gửi email (`Filter Paid Not Sent`).
  - Node `Generate Ticket Data` & `Generate QR Code` (sử dụng API tạo QR) sẽ tạo mã định danh duy nhất (format: `TL-YYYYMMDD-XXXX-N-HASH`) và hình ảnh QR code.
  - Node `Send Email (Gmail)` gửi email HTML chứa mã QR đến khách hàng qua **Gmail OAuth2**.
  - Các node `Update Sheet (Register)` & `Update Sheet (Tickets)` cập nhật trạng thái đã gửi email và lưu thông tin vé.

- **Luồng Quét vé Check-in (`SCAN TICKET` - Webhook):**
  - Node `SCAN TICKET` nhận request POST tại đường dẫn `/v1/scanner`.
  - Node `Parse Barcode` tách `ticket_id` từ dữ liệu quét.
  - Node `Get Tickets` & `Ticket Available?` kiểm tra xem vé có tồn tại và đã được sử dụng hay chưa.
  - Nếu hợp lệ, node `Update Ticket Status` sẽ chuyển trạng thái sang "Checked In" và phản hồi qua node `Checked IN`; nếu đã check-in rồi sẽ báo lỗi qua node `Already Checked IN`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với dữ liệu mẫu cho cả 2 Webhook (`/v1/register` và `/v1/scanner`).
- Bật công tắc **Active** để hệ thống bắt đầu vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Thêm node thông báo về kênh Telegram nội bộ mỗi khi có khách đăng ký thành công hoặc khi có lượt check-in mới tại cổng.
- **Báo cáo doanh thu tự động**: Tạo thêm một nhánh chạy cuối ngày để tổng hợp số lượng vé bán ra và gửi email báo cáo cho ban tổ chức.
- **Bảo mật Webhook**: Thêm header authentication cho các endpoint webhook đăng ký và scanner để tránh bị spam yêu cầu giả mạo.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một hệ thống quản lý sự kiện chuyên nghiệp, tự động hóa từ khâu bán vé đến lúc check-in mà không tốn chi phí cho các bên trung gian thứ ba. Triển khai ngay hôm nay để tối ưu vận hành sự kiện cho doanh nghiệp mình nhé!