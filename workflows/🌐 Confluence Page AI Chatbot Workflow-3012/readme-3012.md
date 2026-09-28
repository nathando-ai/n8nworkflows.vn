---
title: "🤖 [Tự động hóa Chatbot AI cho Confluence Pages] - Giải pháp tự động hóa 100% không cần code"
description: "Hướng dẫn chi tiết cách tự động hóa chatbot AI truy vấn nội dung Confluence Pages bằng n8n. Tiết kiệm thời gian 80% và nâng cao trải nghiệm người dùng với AI chatbot."
slug: "tu-dong-hoa-chatbot-ai-confluence-pages"
tags: [n8n, automation, no-code, confluence, ai-chatbot]
keywords: [n8n workflow, tự động hóa, confluence, ai chatbot, langchain]
---

# 🤖 Tự động hóa Chatbot AI cho Confluence Pages với n8n

[Các sếp đang gặp khó khăn khi phải tìm kiếm thông tin trong hệ thống Confluence Pages thủ công. Với workflow này, các sếp có thể triển khai ngay một chatbot AI truy vấn nội dung Confluence Pages một cách tự động, tiết kiệm thời gian và nâng cao trải nghiệm người dùng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** tìm kiếm thông tin trong Confluence Pages
- Nâng cao trải nghiệm người dùng với chatbot AI tự động trả lời câu hỏi
- Tự động hóa hoàn toàn quy trình truy vấn nội dung
- Tích hợp dễ dàng với các nền tảng tin nhắn như Telegram
- Hỗ trợ nhiều định dạng nội dung (storage, atlas_doc_format, view...)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Confluence với quyền truy cập API
- API Token từ Atlassian (hướng dẫn tạo ở phần dưới)
- Tài khoản OpenAI với API Key
- Tài khoản Telegram (tùy chọn, nếu muốn gửi thông báo qua Telegram)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3012](https://n8n.io/workflows/3012)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "Confluence Page Storage View" và "Search By ID"**
- Cần tạo credentials cho Confluence API:
  1. Truy cập [Atlassian API Tokens](https://id.atlassian.com/manage/api-tokens)
  2. Tạo API Token mới
  3. Trong n8n Editor, tạo credentials mới với loại "HTTP Header Auth"
  4. Điền thông tin:
     - Authentication: Basic Auth
     - User: Email của bạn
     - Password: API Token vừa tạo
  5. Lưu credentials với tên phù hợp (ví dụ: "Confluence API")

**Node "gpt-4o-mini"**
- Cần tạo credentials cho OpenAI API:
  1. Truy cập [OpenAI API Keys](https://platform.openai.com/account/api-keys)
  2. Tạo API Key mới
  3. Trong n8n Editor, tạo credentials mới với loại "OpenAI API"
  4. Điền API Key vừa tạo
  5. Lưu credentials với tên phù hợp (ví dụ: "OpenAI API")

**Node "Send Telegram Message" (tùy chọn)**
- Cần tạo credentials cho Telegram API:
  1. Truy cập [BotFather](https://t.me/BotFather) trên Telegram
  2. Tạo bot mới và nhận API Token
  3. Trong n8n Editor, tạo credentials mới với loại "Telegram API"
  4. Điền API Token vừa nhận
  5. Lưu credentials với tên phù hợp (ví dụ: "Telegram Bot")

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Execute Workflow" để test
2. Kiểm tra kết quả trên các node tương ứng
3. Nếu mọi thứ hoạt động tốt, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Delay" giữa các lần gọi API để tránh bị giới hạn rate
- Tích hợp với Slack hoặc Microsoft Teams thay vì Telegram
- Thêm node "Email" để gửi báo cáo định kỳ về hoạt động của chatbot
- Sử dụng model AI mạnh hơn (gpt-4) nếu cần độ chính xác cao hơn
- Thêm node "Database" để lưu trữ lịch sử truy vấn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa chatbot AI truy vấn nội dung Confluence Pages. Với chỉ 10 phút cấu hình, các sếp có thể triển khai ngay một hệ thống AI chatbot chuyên nghiệp, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để thấy kết quả ngay lập tức!