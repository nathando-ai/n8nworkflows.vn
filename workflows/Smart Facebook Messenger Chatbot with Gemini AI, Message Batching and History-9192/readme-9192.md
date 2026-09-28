---
title: "🤖 Chatbot Facebook thông minh với AI Gemini, gộp tin nhắn và lưu lịch sử"
description: "Tự động hóa chatbot Facebook với AI Gemini, gộp tin nhắn liên tục và lưu lịch sử cuộc trò chuyện - Giải pháp hoàn hảo cho doanh nghiệp cần tương tác khách hàng hiệu quả"
slug: "chatbot-facebook-ai-gemini-gop-tin-nhan-luu-lich-su"
tags: [n8n, automation, no-code, facebook, chatbot, ai, gemini]
keywords: [n8n workflow, tự động hóa, chatbot facebook, ai gemini, gộp tin nhắn, lưu lịch sử]
---

# 🤖 Chatbot Facebook thông minh với AI Gemini, gộp tin nhắn và lưu lịch sử

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải trả lời từng tin nhắn Facebook một cách thủ công. Giới thiệu workflow như giải pháp tự động hóa hoàn toàn không cần code, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công cho mỗi tin nhắn.
- **Gộp tin nhắn thông minh**: Hệ thống tự động gộp các tin nhắn liên tục từ cùng một người dùng.
- **Lưu lịch sử trò chuyện**: Dễ dàng theo dõi và quản lý các cuộc trò chuyện.
- **Trải nghiệm người dùng tốt hơn**: Hiển thị hiệu ứng "đang gõ" và "đã xem" để tạo cảm giác tương tác tự nhiên.
- **Tích hợp AI Gemini**: Cung cấp câu trả lời thông minh và chuyên nghiệp cho khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Developer và một Facebook Page.
- API key từ Google Gemini.
- Token truy cập trang Facebook (Page Access Token).
- n8n phiên bản 1.113.0 trở lên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/9192)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Facebook Webhook**:
   - Cấu hình webhook URL trong Facebook Developer Console: `https://n8n.nguyenthieutoan.com/webhook/nguyenthieutoan-facebook-page`
   - Đặt Verify Token (ví dụ: `jenixToken2025`)

2. **Google Gemini Chat Model**:
   - Thêm credentials cho Google Gemini trong n8n
   - Đảm bảo API key có quyền truy cập đầy đủ

3. **Data Table**:
   - Tạo bảng `Batch_messages` với các cột:
     - `id`: Khóa chính tự động tăng
     - `user_id`: ID người dùng Facebook
     - `user_text`: Nội dung tin nhắn
     - `bot_rep`: Phản hồi của bot
     - `processed`: Trạng thái xử lý (true/false)
     - `createdAt` và `updatedAt`: Thời gian tạo và cập nhật

4. **Facebook API**:
   - Cập nhật Page Access Token trong các node httpRequest liên quan đến Facebook API

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra kết nối Facebook và cấu hình Gemini.
2. Bật Active workflow sau khi đã kiểm tra kỹ các cấu hình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm các node để thông báo khi có tin nhắn mới.
- **Lưu log chi tiết**: Kết nối với Google Sheets hoặc Notion để lưu trữ lịch sử trò chuyện.
- **Gửi báo cáo định kỳ**: Tự động tổng hợp và gửi báo cáo hoạt động của chatbot hàng ngày.
- **Mở rộng tính năng**: Thêm các tính năng như đặt lịch hẹn, kiểm tra lịch trình, hoặc tích hợp với các hệ thống CRM khác.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa chatbot Facebook với AI Gemini, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Với khả năng gộp tin nhắn và lưu lịch sử, nó không chỉ tiết kiệm công sức mà còn giúp doanh nghiệp quản lý tương tác khách hàng một cách hiệu quả hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ chăm sóc khách hàng!