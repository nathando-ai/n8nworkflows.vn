---
title: "🚀 Tự động hóa chiến dịch Drive-To-Store & phát Coupon với n8n, Google Sheets và SuiteCRM"
description: "Xây dựng hệ thống thu thập Lead qua Form, tự động kiểm tra trùng lặp, cấp mã Coupon từ Google Sheets và đồng bộ dữ liệu vào SuiteCRM hoàn toàn tự động."
slug: "tu-dong-hoa-drive-to-store-lead-generation-suitecrm-google-sheets"
tags: [n8n, automation, crm, suitecrm, google-sheets, lead-generation]
keywords: [n8n workflow, drive to store, suitecrm integration, google sheets coupon, tu dong hoa marketing]
---

# 🚀 Tự động hóa chiến dịch Drive-To-Store & phát Coupon với n8n

Trong các chiến dịch Marketing "Drive-To-Store" (kéo khách từ online về cửa hàng offline), việc tặng mã giảm giá (coupon) qua form đăng ký là cách cực kỳ hiệu quả để thu hút khách hàng. Tuy nhiên, việc thủ công kiểm tra xem khách hàng đã nhận mã chưa, cấp mã độc nhất, rồi đẩy thông tin lên CRM thường tốn rất nhiều thời gian và dễ xảy ra sai sót.

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình trên: Nhận thông tin từ Form/Webhook, kiểm tra khách hàng trùng lặp trên Google Sheets, tự động lấy mã coupon chưa sử dụng, đồng thời tạo Lead mới kèm coupon trên hệ thống SuiteCRM.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Khách hàng điền form là nhận ngay coupon và được lưu trữ trên CRM mà không cần nhân sự can thiệp.
- **Chống gian lận/trùng lặp:** Hệ thống tự động check xem email/số điện thoại đã nhận coupon chưa (`Duplicate Lead?` & `Is Duplicate?`).
- **Quản lý kho Coupon thông minh:** Tự động quét và lấy mã coupon chưa gán từ Google Sheets.
- **Đồng bộ CRM mượt mà:** Đẩy dữ liệu Lead trực tiếp vào SuiteCRM (hỗ trợ cả phiên bản 7.14.x và 8.x).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Google Sheets:** Tạo sẵn một bảng tính chứa danh sách mã coupon (Tham khảo mẫu Google Sheet từ tác giả).
- **SuiteCRM:** Đã tạo sẵn trường dữ liệu tùy chỉnh (custom field) tên là `coupon` trong module Leads. Lấy thông tin API OAuth2 (`CLIENTID`, `CLIENTSECRET` và `SUITECRMURL`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor (hoặc import file JSON thông qua giao diện n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Sheets Nodes (`Duplicate Lead?`, `Get Coupon`, `Update Lead`):** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Trỏ đến file Google Sheet quản lý coupon của các sếp.
  - Cấu hình node `Update Lead` ở chế độ `update` để đánh dấu mã coupon đã được sử dụng/gán cho khách.
- **SuiteCRM Nodes (`Token SuiteCRM`, `Create Lead SuiteCRM`):**
  - Cấu hình các biến HTTP Request gọi API SuiteCRM.
  - Thay thế các giá trị `SUITECRMURL`, `CLIENTSECRET`, và `CLIENTID` bằng thông tin thực tế của hệ thống CRM.
  - *Cách lấy Client Credentials:* Vào SuiteCRM chọn `Admin` -> `OAuth2 Client and Token` -> Click `New Client Credentials Client`. (Xem thêm tài liệu chính thức từ SuiteCRM nếu cần).
- **Trigger Nodes (`On form submission` hoặc `Webhook`):**
  - Nếu dùng form tích hợp sẵn trong n8n, sử dụng `On form submission`.
  - Nếu dùng form bên ngoài (Landing page riêng), hãy cấu hình nhận dữ liệu qua node `Webhook`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Execute Workflow`) với dữ liệu mẫu để kiểm tra luồng từ Form -> Google Sheets -> SuiteCRM.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi Email tự động:** Thêm node gửi email (Gmail/SMTP) ngay sau khi lấy được coupon để gửi mã giảm giá trực tiếp vào hộp thư của khách hàng.
- **Thông báo qua Telegram/Slack:** Thêm node thông báo để đội ngũ Sales nắm bắt ngay khi có một Lead mới vừa nhận coupon và đổ về CRM.
- **Lưu log lỗi:** Thiết lập nhánh lỗi (Error Trigger) để cảnh báo qua chat nếu quá trình gọi API SuiteCRM gặp sự cố.

### 📌 Kết luận
Workflow này là giải pháp "phải có" cho các chiến dịch marketing thu hút khách hàng offline thông qua mã giảm giá. Hãy triển khai ngay để tối ưu hóa tỷ lệ chuyển đổi và giải phóng sức lao động cho đội ngũ vận hành!