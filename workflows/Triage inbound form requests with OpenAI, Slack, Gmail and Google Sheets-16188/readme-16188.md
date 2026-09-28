---
title: "🚀 Tự động phân loại và trả lời tự động các yêu cầu liên hệ từ website bằng OpenAI, Slack, Gmail và Google Sheets"
description: "Hướng dẫn tự động hóa quy trình xử lý các yêu cầu liên hệ từ website bằng n8n, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-phan-loai-tra-loi-tu-dong-yeu-cau-lien-he"
tags: [n8n, automation, no-code, openai, google-sheets]
keywords: [n8n workflow, tự động hóa, openai, google sheets, xử lý liên hệ]
---

# 🚀 Tự động phân loại và trả lời tự động các yêu cầu liên hệ từ website bằng OpenAI, Slack, Gmail và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại các yêu cầu liên hệ thành các danh mục (hỗ trợ, báo giá, khiếu nại...)
- Tự động trả lời khách hàng bằng nội dung được tạo bởi OpenAI
- Tự động thông báo đến nhóm hỗ trợ qua Slack
- Tự động lưu trữ và quản lý dữ liệu liên hệ trên Google Sheets
- Tiết kiệm thời gian xử lý thủ công lên đến 90%
- Tăng trải nghiệm khách hàng với thời gian phản hồi nhanh chóng
- Có được dữ liệu thống kê và phân tích về các yêu cầu liên hệ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key
- Tài khoản Google với quyền truy cập Gmail và Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- Form liên hệ trên website đã cấu hình để gửi dữ liệu qua HTTP POST
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/16188`
4. Nhấn "OK" để hoàn tất quá trình import

Hoặc bạn có thể:
1. Truy cập vào link: https://n8n.io/workflows/16188
2. Nhấn vào nút "Download" để tải file JSON về máy
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Receive Form Submission" (Webhook)**:
   - Đảm bảo URL webhook được cấu hình đúng với endpoint của form liên hệ trên website
   - Kiểm tra xem form liên hệ đã được cấu hình để gửi dữ liệu dưới dạng JSON với các trường: name, email, message

2. **Node "Classify & Draft Reply" (OpenAI)**:
   - Thêm credentials cho OpenAI
   - Cấu hình prompt để OpenAI trả về kết quả dưới dạng JSON với các trường: category, urgency, sentiment, summary, suggested_reply
   - Ví dụ prompt:
     ```
     You are a helpful assistant that classifies contact form submissions.
     Analyze the following message and return a JSON object with these fields:
     - category: one of "support", "quote", "complaint", "other"
     - urgency: one of "low", "medium", "high"
     - sentiment: one of "positive", "neutral", "negative"
     - summary: a brief summary of the message
     - suggested_reply: a polite and professional reply to the sender

     Message: {{ $node["Receive Form Submission"].json["message"] }}
     ```

3. **Node "Log Spam" và "Log Submission" (Google Sheets)**:
   - Thêm credentials cho Google Sheets
   - Chỉ định ID của Google Sheet và tên của Sheet cần ghi dữ liệu
   - Đảm bảo các cột trong Sheet đã được đặt tên đúng với các trường dữ liệu: timestamp, name, email, category, urgency, sentiment, summary, message

4. **Node "Alert Team" (Slack)**:
   - Thêm credentials cho Slack
   - Chọn channel cần gửi thông báo
   - Cấu hình nội dung thông báo để bao gồm các thông tin quan trọng từ yêu cầu liên hệ

5. **Node "Send AI Auto-Reply" (Gmail)**:
   - Thêm credentials cho Gmail
   - Cấu hình email gửi đi (nếu cần)
   - Đảm bảo nội dung email sử dụng trường suggested_reply từ kết quả của OpenAI

#### 3. Kích hoạt ⚡️
1. Sau khi hoàn tất cấu hình các node quan trọng, nhấn vào nút "Execute Workflow" để kiểm tra hoạt động của workflow
2. Gửi một yêu cầu liên hệ thử từ form liên hệ trên website
3. Kiểm tra kết quả trên Slack, Gmail và Google Sheets
4. Nếu mọi thứ hoạt động đúng, nhấn vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi thông báo qua Telegram hoặc Discord thay vì Slack
- Cấu hình để gửi báo cáo hàng ngày về các yêu cầu liên hệ qua email
- Thêm node để lưu trữ các yêu cầu liên hệ vào cơ sở dữ liệu thay vì Google Sheets
- Tích hợp với các hệ thống CRM khác như HubSpot, Salesforce
- Cấu hình để gửi email nhắc nhở cho khách hàng nếu yêu cầu của họ chưa được xử lý trong thời gian quy định

### 📌 Kết luận
Workflow này giúp tự động hóa toàn bộ quy trình xử lý các yêu cầu liên hệ từ website, từ phân loại và trả lời tự động đến thông báo và lưu trữ dữ liệu. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian xử lý thủ công, nâng cao trải nghiệm khách hàng và có được dữ liệu thống kê hữu ích cho việc quản lý và phát triển kinh doanh.