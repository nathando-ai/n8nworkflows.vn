---
title: "🚀 Tự động giám sát thiết bị y tế với Google Sheets, WhatsApp và Email bằng n8n"
description: "Xây dựng hệ thống giám sát thiết bị y tế tự động chạy định kỳ 6h sáng, phân tích dữ liệu từ Google Sheets, gửi cảnh báo qua WhatsApp, Email cho kỹ thuật viên và cấp quản lý."
slug: "giam-sat-thiet-bi-y-te-google-sheets-whatsapp-email-n8n"
tags: [n8n, automation, no-code, google-sheets, whatsapp, healthcare]
keywords: [n8n workflow, giám sát thiết bị y tế, tự động hóa google sheets, cảnh báo whatsapp email, n8n template]
---

# 🚀 Tự động giám sát thiết bị y tế với Google Sheets, WhatsApp và Email

Trong môi trường y tế, việc kiểm tra và bảo trì thiết bị đúng hạn đóng vai trò sống còn. Tuy nhiên, việc theo dõi thủ công danh sách hàng trăm thiết bị qua Excel hay Google Sheets rất dễ dẫn đến sai sót, bỏ quên lịch bảo trì, gây ảnh hưởng nghiêm trọng đến quy trình vận hành. 

Giải pháp? Một hệ thống tự động hóa 100% không cần code được phát triển bởi **Oneclick AI Squad**, giúp tự động quét dữ liệu, phân loại mức độ cảnh báo và gửi thông báo tức thì đến kỹ thuật viên lẫn cấp quản lý mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Hệ thống tự động kiểm tra thiết bị vào 6h sáng mỗi ngày mà không cần nhắc nhở.
- **Phân tầng cảnh báo thông minh:** Gửi thông báo bảo trì thường cho kỹ thuật viên và leo thang cảnh báo khẩn cấp (Critical) cho cấp quản lý.
- **Đa kênh tiếp cận:** Kết hợp linh hoạt giữa Email truyền thống và WhatsApp để đảm bảo không bỏ sót thông tin.
- **Đồng bộ dữ liệu thời gian thực:** Tự động cập nhật trạng thái thiết bị và ghi log bảo trì trực tiếp vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets & Google API Credentials:** File Google Sheets chứa danh sách thiết bị y tế và quyền truy cập API.
- **SMTP Server / Email Account:** Tài khoản SMTP (Gmail, SendGrid, Office365...) để gửi email cảnh báo.
- **WhatsApp Business API:** Tài khoản WhatsApp API để gửi tin nhắn tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này hoặc tải file từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau trước khi chạy:
- **Daily Equipment Check (6 AM) (Cron):** Node kích hoạt lịch chạy. Có thể chỉnh lại múi giờ (Timezone) hoặc thời gian chạy nếu cần.
- **Read Equipment Data, Log Maintenance Alerts, Update Equipment Status (Google Sheets):** 
  - Kết nối tài khoản Google API Credentials.
  - Trỏ đúng file Google Sheets quản lý thiết bị và chọn đúng Sheet Name/Range tương ứng.
- **Process Equipment Alerts (Code):** Node JavaScript xử lý logic kiểm tra hạn bảo trì và lọc ra các thiết bị cần chú ý.
- **Send Technician Email & Send Critical Alert to Supervisors (Email Send):** Chọn credentials SMTP đã chuẩn bị và điền địa chỉ email nhận tin của kỹ thuật viên / quản lý.
- **Send message & Send Critical Alert Massage (WhatsApp):** Kết nối tài khoản WhatsApp API, cấu hình số điện thoại nhận tin và template tin nhắn phù hợp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công với dữ liệu mẫu trong Google Sheets và kiểm tra xem Email/WhatsApp đã được gửi thành công chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatops:** Thêm node Telegram hoặc Slack để gửi bản tin tóm tắt tổng quan tình trạng thiết bị vào nhóm chung của phòng kỹ thuật.
- **Tạo Dashboard trực quan:** Kết hợp dữ liệu log bảo trì từ Google Sheets để dựng dashboard trên Looker Studio (Google Data Studio) theo dõi hiệu suất thiết bị theo tháng/quý.
- **Cơ chế Retry:** Bật tính năng Error Workflow trong n8n để tự động ping kỹ thuật viên qua kênh phụ nếu việc gọi WhatsApp API gặp lỗi.

### 📌 Kết luận
Với workflow giám sát thiết bị y tế này, các sếp đã số hóa thành công quy trình quản lý tài sản, giảm thiểu tối đa rủi ro hỏng hóc thiết bị đột xuất. "Lên đồ" ngay cho hệ thống của mình thôi nào!