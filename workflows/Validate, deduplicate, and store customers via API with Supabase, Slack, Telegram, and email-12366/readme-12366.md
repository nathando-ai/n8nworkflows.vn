---
title: "🚀 Tự động hóa CRM: Xác thực, loại bỏ trùng lặp và lưu khách hàng qua API với Supabase, Slack, Telegram và Email"
description: "Hướng dẫn tự động hóa quy trình xác thực khách hàng, loại bỏ trùng lặp và lưu dữ liệu vào Supabase thông qua API, với thông báo tự động qua Slack, Telegram và Email"
slug: "tu-dong-hoa-crm-xac-thuc-khach-hang-supabase-slack-telegram-email"
tags: [n8n, automation, no-code, crm, ai]
keywords: [n8n workflow, tự động hóa crm, xác thực khách hàng, loại bỏ trùng lặp, supabase, slack, telegram, email]
---

# 🚀 Tự động hóa CRM: Xác thực, loại bỏ trùng lặp và lưu khách hàng qua API với Supabase, Slack, Telegram và Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý khách hàng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian quản lý khách hàng thủ công
- Giảm 90% lỗi nhập liệu nhờ xác thực tự động
- Loại bỏ hoàn toàn trùng lặp khách hàng
- Nhận thông báo tức thì qua Slack, Telegram và Email
- Tự động hóa quy trình CRM hoàn toàn không cần lập trình
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Supabase với bảng `customers` đã được cấu hình
- API Key của Supabase với quyền đọc/ghi
- Tài khoản Slack và API Key
- Tài khoản Telegram và Bot Token
- Tài khoản Gmail và OAuth2 credentials
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12366](https://n8n.io/workflows/12366)
2. Nhấn nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Nhấn "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Customer API1" (Webhook)**:
   - Đảm bảo cấu hình đúng path: `/customer/validate-and-store`
   - Chọn HTTP Method: `POST`

2. **Node "Check Existing User" và "Create User" (Supabase)**:
   - Cấu hình credentials `supabaseApi`
   - Đảm bảo bảng `customers` trong Supabase có các trường: `email`, `first_name`, `last_name`, `phone`

3. **Node "Slack Notify" (Slack)**:
   - Cấu hình credentials `slackApi`
   - Chọn channel để nhận thông báo

4. **Node "Telegram Notify" (Telegram)**:
   - Cấu hình credentials `telegramApi`
   - Nhập Chat ID của người nhận thông báo

5. **Node "Send Notifiaction to User" (Gmail)**:
   - Cấu hình credentials `gmailOAuth2`
   - Thiết lập template email cho thông báo thành công

6. **Node "Validate & Clean Data" (Code)**:
   - Kiểm tra và điều chỉnh logic JavaScript nếu cần xử lý đặc biệt cho dữ liệu khách hàng
   - Đảm bảo các trường bắt buộc được kiểm tra: `email`, `first_name`, `last_name`

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra các node respondToWebhook để đảm bảo phản hồi API đúng
3. Bật chế độ "Active" cho workflow khi đã test thành công

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node "AI Summarization" để tự động tạo báo cáo hàng ngày về khách hàng mới
2. Kết nối với CRM khác như HubSpot hoặc Salesforce để đồng bộ dữ liệu
3. Thiết lập báo cáo định kỳ gửi qua Email với tổng hợp khách hàng mới
4. Tích hợp với hệ thống chatbot để tự động xử lý yêu cầu từ khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình quản lý khách hàng, từ xác thực dữ liệu đến lưu trữ và thông báo. Với việc tích hợp Supabase, Slack, Telegram và Email, các sếp có thể quản lý khách hàng hiệu quả hơn, giảm thiểu lỗi và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!