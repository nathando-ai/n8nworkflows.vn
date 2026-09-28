---
title: "🚀 Tự động gửi tin nhắn WhatsApp theo dõi khách hàng mới từ form"
description: "Hướng dẫn tự động hóa gửi tin nhắn WhatsApp và ghi log khách hàng mới vào Google Sheets khi có lead mới từ form"
slug: "tu-dong-gui-tin-nhan-whatsapp-theo-doi-khach-hang-moi-tu-form"
tags: [n8n, automation, no-code, whatsapp, google-sheets]
keywords: [n8n workflow, tự động hóa, whatsapp marketing, lead nurturing]
---

# 🚀 Tự động gửi tin nhắn WhatsApp theo dõi khách hàng mới từ form

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý thủ công
- Tăng tốc độ phản hồi với khách hàng mới
- Theo dõi lead một cách chuyên nghiệp
- Tích hợp liền mạch giữa form và WhatsApp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản MoltFlow đã kết nối WhatsApp
- Form có sẵn (Typeform, JotForm, Google Forms, hoặc bất kỳ form nào có thể POST webhook)
- API Key từ MoltFlow
- Tài khoản Google đã kích hoạt Google Sheets API
- Thông tin xác thực Google Sheets OAuth 2.0
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13480](https://n8n.io/workflows/13480)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Form Submission Webhook** node:
   - Đảm bảo webhook URL được cấu hình đúng trong form của bạn
   - Kiểm tra lại method POST

2. **Parse Form Data** node:
   - Thay đổi `YOUR_SESSION_ID` thành session ID thực tế từ MoltFlow
   - Đảm bảo các trường dữ liệu từ form được ánh xạ đúng với biến trong code

3. **Send WhatsApp Follow-up** node:
   - Thêm credentials `httpHeaderAuth` với API Key từ MoltFlow
   - Kiểm tra lại URL endpoint của MoltFlow

4. **Log Lead to Sheet** node:
   - Thêm credentials `googleSheetsOAuth2Api`
   - Cấu hình sheet ID và tên sheet chính xác
   - Đảm bảo các trường dữ liệu được ánh xạ đúng với cột trong Google Sheets

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi có lead mới
- Tích hợp với CRM như HubSpot hoặc Salesforce
- Thiết lập các quy tắc khác nhau cho các loại lead khác nhau
- Tự động hóa gửi tin nhắn theo dõi sau 1 ngày, 3 ngày, 1 tuần...

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi lead một cách chuyên nghiệp, tiết kiệm thời gian và tăng tốc độ phản hồi với khách hàng mới. Hãy thử ngay để thấy sự khác biệt!