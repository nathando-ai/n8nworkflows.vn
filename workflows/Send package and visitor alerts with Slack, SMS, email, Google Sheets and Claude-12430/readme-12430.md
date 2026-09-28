---
title: "🚀 Tự động hóa cảnh báo gói hàng và khách truy cập với Slack, SMS, Email, Google Sheets và Claude"
description: "Workflow n8n tự động theo dõi gói hàng và khách truy cập, thông báo qua email/SMS, cảnh báo quản lý qua Slack và ghi log vào Google Sheets. Giải pháp toàn diện cho quản lý tài sản."
slug: "tu-dong-hoa-canh-bao-goi-hang-khach-truy-cap"
tags: [n8n, automation, no-code, slack, sms, google-sheets, ai]
keywords: [n8n workflow, tự động hóa, quản lý tài sản, cảnh báo gói hàng, khách truy cập]
---

# 🚀 Tự động hóa cảnh báo gói hàng và khách truy cập với Slack, SMS, Email, Google Sheets và Claude

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp quản lý tài sản khi phải theo dõi thủ công gói hàng và khách truy cập. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thông báo gói hàng và khách truy cập qua email/SMS
- Cảnh báo quản lý qua Slack với mức độ ưu tiên
- Ghi log đầy đủ vào Google Sheets cho báo cáo
- Tiết kiệm 80% thời gian theo dõi thủ công
- Đảm bảo thông tin được xử lý nhanh chóng và chính xác
- Tích hợp AI để phân loại mức độ ưu tiên thông báo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản email để gửi thông báo
- API key từ dịch vụ SMS (ví dụ: SMS77)
- Tài khoản Google với quyền truy cập Google Sheets
- API key từ Anthropic để sử dụng Claude AI
- Hệ thống quản lý gói hàng/khách truy cập có thể kết nối với webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12430](https://n8n.io/workflows/12430)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Package/Visitor Webhook**:
   - Cấu hình webhook endpoint: `/package-visitor-webhook`
   - Đảm bảo hệ thống quản lý gói hàng/khách truy cập có thể gửi dữ liệu đến webhook này

2. **Workflow Configuration**:
   - Cấu hình các tham số chung cho workflow như email mặc định, số điện thoại quản lý...

3. **Anthropic Chat Model** (2 node):
   - Đảm bảo đã tạo tài khoản và có API key từ Anthropic
   - Chọn model "Claude Sonnet 4.5" trong node này
   - Cấu hình credentials cho Anthropic trong n8n

4. **Email Tenant - High Urgency** và **Email Tenant - Regular**:
   - Cấu hình SMTP credentials cho email gửi thông báo
   - Điền địa chỉ email nhận thông báo (có thể sử dụng biểu thức để lấy từ dữ liệu đầu vào)

5. **SMS Tenant - High Urgency**:
   - Cấu hình credentials cho dịch vụ SMS (ví dụ: SMS77)
   - Điền số điện thoại nhận thông báo (có thể sử dụng biểu thức để lấy từ dữ liệu đầu vào)

6. **Notify Management**:
   - Cấu hình credentials cho Slack
   - Chọn channel để gửi thông báo
   - Tùy chỉnh nội dung thông báo theo nhu cầu

7. **Log to Google Sheets**:
   - Cấu hình credentials cho Google Sheets
   - Chọn spreadsheet và worksheet để ghi log
   - Đảm bảo có quyền ghi dữ liệu vào sheet này

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kiểm tra các thông báo được gửi đến email, SMS và Slack
3. Xác nhận dữ liệu được ghi đúng vào Google Sheets
4. Bật Active workflow khi đã kiểm tra và xác nhận mọi thứ hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh mức độ ưu tiên**: Điều chỉnh prompt trong node "Classify Urgency" để phù hợp với tiêu chí ưu tiên của các sếp
2. **Kết hợp với Telegram**: Thêm node Telegram để nhận thông báo bổ sung
3. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp từ Google Sheets
4. **Xử lý lỗi**: Thêm node xử lý lỗi để gửi cảnh báo khi workflow gặp sự cố
5. **Tích hợp với hệ thống CRM**: Kết nối với CRM để quản lý thông tin khách hàng và lịch sử giao dịch

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc quản lý gói hàng và khách truy cập, giúp các sếp tiết kiệm thời gian và đảm bảo thông tin được xử lý nhanh chóng và chính xác. Bằng cách tích hợp các công cụ thông báo và AI, workflow này không chỉ tự động hóa quy trình mà còn nâng cao hiệu quả quản lý tài sản.