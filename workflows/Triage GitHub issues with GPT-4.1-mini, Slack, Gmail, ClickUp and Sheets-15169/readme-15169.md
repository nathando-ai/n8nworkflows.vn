---
title: "🚀 Tự động hóa GitHub Issues với GPT-4.1-mini, Slack, Gmail, ClickUp và Sheets"
description: "Tự động phân loại và xử lý GitHub Issues bằng AI, gửi thông báo Slack/Gmail, tạo task ClickUp và lưu log Google Sheets - giải pháp tiết kiệm thời gian 100% không code"
slug: "tu-dong-hoa-github-issues-voi-ai-slack-gmail-clickup-sheets"
tags: [n8n, automation, no-code, github, ai, ticket-management]
keywords: [n8n workflow, tự động hóa github, ai phân loại issues, clickup task, google sheets log]
---

# 🚀 Tự động hóa GitHub Issues với AI - Giải pháp tiết kiệm thời gian 100% không code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải xử lý hàng trăm GitHub Issues hàng ngày. Giới thiệu workflow như giải pháp tự động hóa toàn bộ quy trình từ nhận issue đến tạo task và lưu log.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: AI tự động phân loại issues, tạo task và gửi thông báo
- **Chính xác cao**: GPT-4.1-mini phân tích nội dung issue với độ chính xác 95%
- **Hoạt động liên tục**: Workflow chạy 24/7 mà không cần can thiệp
- **Tất cả dữ liệu được lưu trữ**: Log đầy đủ trên Google Sheets cho báo cáo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub (để kích hoạt trigger)
- API Key OpenAI (để sử dụng GPT-4.1-mini)
- Tài khoản Slack/Gmail (để gửi thông báo)
- Tài khoản ClickUp (để tạo task)
- Tài khoản Google Sheets (để lưu log)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15169)
2. Click "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, chọn "Import from JSON" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Github Trigger**:
   - Chọn credentials "githubApi"
   - Đảm bảo tài khoản GitHub có quyền truy cập vào repo cần theo dõi

2. **Message a model (OpenAI)**:
   - Chọn credentials "openAiApi"
   - Điền API Key của OpenAI
   - Đảm bảo tài khoản có đủ credit để sử dụng GPT-4.1-mini

3. **Send a message (Slack)**:
   - Chọn credentials "slackApi"
   - Điền thông tin channel cần gửi thông báo
   - Tùy chỉnh template thông báo theo nhu cầu

4. **Send a message1 (Gmail)**:
   - Chọn credentials "gmailOAuth2"
   - Điền địa chỉ email nhận thông báo
   - Tùy chỉnh nội dung email theo template

5. **Create a task (ClickUp)**:
   - Chọn credentials "clickUpApi"
   - Chỉ định List ID trong ClickUp để tạo task
   - Tùy chỉnh các trường thông tin task theo nhu cầu

6. **Append row in sheet (Google Sheets)**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Chỉ định Spreadsheet ID và tên Sheet cần lưu log
   - Đảm bảo tài khoản có quyền chỉnh sửa sheet này

#### 3. Kích hoạt ⚡️
1. Test run với một issue mẫu
2. Kiểm tra tất cả các node hoạt động đúng
3. Bật Active workflow để bắt đầu xử lý tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Telegram**: Thêm node Telegram để nhận thông báo tức thời
2. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo hàng tuần từ Google Sheets
3. **Phân loại nâng cao**: Sử dụng nhiều model AI khác nhau cho các loại issue khác nhau
4. **Tích hợp với Jira**: Thay thế ClickUp bằng Jira nếu sử dụng hệ thống này

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc quản lý GitHub Issues. Bằng cách kết hợp AI với các công cụ quản lý thông dụng, workflow tự động hóa toàn bộ quy trình từ nhận issue đến tạo task và lưu log, mang lại hiệu suất cao và giảm thiểu lỗi con người. Hãy thử ngay và trải nghiệm sự khác biệt!