---
title: "🤖 Tự động hóa CSKH WhatsApp với AI Gemini: Xử lý Text & Voice cùng Knowledge Base"
description: "Hướng dẫn chi tiết cách triển khai workflow n8n tự động hóa CSKH WhatsApp với AI Gemini, xử lý cả tin nhắn văn bản và giọng nói cùng cơ sở kiến thức doanh nghiệp"
slug: "tu-dong-hoa-cskh-whatsapp-voi-ai-gemini"
tags: [n8n, automation, no-code, whatsapp, ai]
keywords: [n8n workflow, tự động hóa, chatbot, whatsapp, ai]
---

# 🤖 Tự động hóa CSKH WhatsApp với AI Gemini: Xử lý Text & Voice cùng Knowledge Base

[Các sếp] có biết không? Hàng ngày, các đội CSKH phải xử lý hàng trăm tin nhắn WhatsApp, từ các câu hỏi đơn giản đến các yêu cầu phức tạp về sản phẩm/dịch vụ. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này với AI Gemini, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Xử lý cả tin nhắn văn bản và giọng nói
- **Trả lời chính xác**: Kết nối với cơ sở kiến thức doanh nghiệp thông qua Pinecone
- **Nhớ lịch sử**: Giữ trạng thái hội thoại để trả lời liên quan
- **Tiết kiệm thời gian**: Giảm tới 80% thời gian xử lý tin nhắn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API
- API Key từ Google Gemini
- Tài khoản Pinecone để lưu trữ cơ sở kiến thức
- Dữ liệu sản phẩm/dịch vụ đã được vector hóa trong Pinecone
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10033](https://n8n.io/workflows/10033)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **WhatsApp Trigger**:
   - Cấu hình credentials cho "whatsAppTriggerApi"
   - Điền số điện thoại WhatsApp Business của doanh nghiệp

2. **Google Gemini Chat Model**:
   - Cấu hình credentials cho "googlePalmApi"
   - Điền API Key từ Google Cloud Console

3. **Pinecone Vector Store**:
   - Cấu hình credentials cho "pineconeApi"
   - Điền thông tin kết nối Pinecone (Environment, Index Name)

4. **Embeddings Google Gemini**:
   - Đảm bảo đã cấu hình credentials "googlePalmApi" như bước 2

5. **Audio Download**:
   - Cấu hình credentials "httpHeaderAuth" với các header cần thiết để tải file âm thanh

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu:
   - Gửi tin nhắn văn bản và giọng nói đến số WhatsApp của doanh nghiệp
   - Kiểm tra kết quả trả về từ AI Agent

2. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối Slack/Telegram**: Thêm node để thông báo khi có tin nhắn mới
2. **Báo cáo hàng ngày**: Thêm node để tổng hợp và gửi báo cáo hoạt động CSKH
3. **Tích hợp CRM**: Kết nối với Salesforce/Huub để lưu trữ thông tin khách hàng
4. **Xử lý đa ngôn ngữ**: Thêm node để dịch tự động giữa các ngôn ngữ

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa CSKH trên WhatsApp với AI Gemini. Với khả năng xử lý cả văn bản và giọng nói cùng cơ sở kiến thức doanh nghiệp, các sếp có thể nâng cao hiệu suất CSKH và trải nghiệm khách hàng một cách đáng kể. Hãy triển khai ngay để thấy kết quả ngay lập tức!