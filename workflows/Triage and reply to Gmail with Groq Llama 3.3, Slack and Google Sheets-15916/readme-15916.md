---
title: "🚀 Tự động phân loại email Gmail và trả lời tự động với Groq, Slack và Google Sheets"
description: "Workflow n8n tự động phân loại email, trả lời tự động bằng AI và ghi log vào Google Sheets - tiết kiệm 80% thời gian xử lý email thủ công"
slug: "tu-dong-phan-loai-email-gmail-groq-slack-google-sheets"
tags: [n8n, automation, no-code, gmail, slack, google-sheets]
keywords: [n8n workflow, tự động hóa email, phân loại email, AI tự động trả lời, quản lý ticket]
---

# 🚀 Tự động phân loại email Gmail và trả lời tự động với Groq, Slack và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại email thành 3 loại: Khẩn cấp, Bán hàng, Thông thường
- Tự động trả lời email bằng AI (Groq Llama 3.3) với nội dung cá nhân hóa
- Ghi log toàn bộ quá trình xử lý vào Google Sheets
- Thông báo tự động lên Slack với nội dung email đã được tóm tắt
- Tiết kiệm 80% thời gian xử lý email thủ công
- Đảm bảo không bỏ sót bất kỳ email quan trọng nào
- Tạo báo cáo tự động về hoạt động email hàng ngày
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail (cần quyền truy cập đầy đủ)
- API Key từ Groq (đăng ký tại [console.groq.com](https://console.groq.com))
- Slack Bot Token (tạo tại [api.slack.com](https://api.slack.com))
- Google Sheets (cần tạo trước bảng tính để lưu log)
- Tạo 2 kênh Slack: #incidents và #sales
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15916)
2. Click vào nút "Import" và chọn "Import from URL"
3. Copy URL workflow và dán vào ô nhập liệu
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Gmail – New Email"**:
   - Cấu hình credentials Gmail OAuth2
   - Đặt thời gian kiểm tra email (mặc định 1 phút)

2. **Node "Claude – Classify & Draft"**:
   - Thêm Groq API Key vào HTTP Header Auth
   - URL endpoint: `https://api.groq.com/openai/v1/chat/completions`
   - Thêm header: `Authorization: Bearer YOUR_GROQ_API_KEY`
   - Tham số body:
     ```json
     {
       "model": "llama3-8b-8192",
       "messages": [
         {
           "role": "system",
           "content": "You are a helpful assistant that classifies emails and drafts replies."
         },
         {
           "role": "user",
           "content": "Classify this email into one of these categories: Critical, Sales, Normal. Then draft a reply. Email content: {{ $node["Gmail – New Email"].json["text"] }}"
         }
       ]
     }
     ```

3. **Node "Slack – Post to #incidents" và "Slack – Post to #sales"**:
   - Cấu hình Slack API credentials
   - Đảm bảo bot có quyền post vào các kênh này

4. **Node "Sheets – Log Triage"**:
   - Cấu hình Google Sheets OAuth2
   - Chỉ định Sheet ID và tên sheet cần ghi log
   - Cấu hình các cột dữ liệu cần ghi (Subject, From, Date, Classification, Reply)

5. **Node "Gmail – Critical Alert Email"**:
   - Cấu hình email gửi cảnh báo khẩn cấp
   - Đặt địa chỉ email nhận cảnh báo

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click "Activate" để chạy workflow
3. Để theo dõi hoạt động, sử dụng tab "Executions" trong n8n

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh phân loại email**:
   - Chỉnh sửa prompt trong node "Claude – Classify & Draft" để thêm các loại email mới
   - Ví dụ: "Support", "Marketing", "HR"

2. **Kết nối thêm dịch vụ**:
   - Thêm node để gửi thông báo qua Telegram
   - Kết nối với CRM để tạo ticket tự động
   - Gửi báo cáo hàng ngày qua email

3. **Tối ưu hiệu suất**:
   - Tăng thời gian kiểm tra email lên 5 phút nếu lượng email không quá lớn
   - Sử dụng queue mode để xử lý email theo thứ tự ưu tiên

4. **Bảo mật nâng cao**:
   - Thiết lập IP whitelist cho các API key
   - Sử dụng 2FA cho tất cả tài khoản dịch vụ liên quan

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc quản lý email. Bằng cách tự động phân loại, trả lời và ghi log, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn. Hãy thử ngay và trải nghiệm sự khác biệt trong cách quản lý email của bạn!