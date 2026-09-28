---
title: "🤖 Chatbot Trí tuệ nhân tạo với CSDL Google Drive sử dụng GPT-4 và Mistral AI"
description: "Hướng dẫn tự động hóa chatbot hỗ trợ khách hàng với cơ sở kiến thức từ Google Drive, tích hợp OCR và trí tuệ nhân tạo"
slug: "chatbot-google-drive-gpt4-mistral-ai"
tags: [n8n, automation, no-code, chatbot, ai]
keywords: [n8n workflow, tự động hóa chatbot, trí tuệ nhân tạo, google drive, mistral ai]
---

# 🤖 Chatbot Trí tuệ nhân tạo với CSDL Google Drive sử dụng GPT-4 và Mistral AI

[Các sếp đang gặp khó khăn khi phải trả lời các câu hỏi khách hàng liên tục từ nhiều nguồn tài liệu khác nhau trên Google Drive. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ lấy dữ liệu đến trả lời câu hỏi thông minh, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình xử lý tài liệu từ Google Drive
- Tích hợp OCR thông minh từ Mistral AI để xử lý tài liệu quét
- Tạo cơ sở kiến thức vector với Qdrant cho tìm kiếm ngữ nghĩa
- Trả lời câu hỏi khách hàng một cách chính xác và liên tục 24/7
- Tiết kiệm thời gian xử lý tài liệu lên tới 90%
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với các tài liệu cần xử lý
- API Key từ OpenAI (cho GPT-4)
- API Key từ Mistral AI (cho OCR và embeddings)
- Tài khoản Qdrant (hoặc cài đặt self-hosted)
- Tài khoản n8n (self-hosted hoặc cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10142](https://n8n.io/workflows/10142)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow
4. Hoàn tất import và mở workflow trong editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When chat message received" (chatTrigger)**
   - Cấu hình webhook endpoint cho chatbot của bạn
   - Đảm bảo endpoint này được bảo mật

2. **Node "OpenAI Chat Model" (lmChatOpenAi)**
   - Thêm credentials OpenAI API
   - Chọn model GPT-4.1-mini (hoặc model khác phù hợp)
   - Cấu hình các tham số như temperature, max tokens...

3. **Node "Qdrant Vector Store" (vectorStoreQdrant)**
   - Thêm credentials Qdrant API
   - Tạo hoặc chọn collection để lưu trữ vector embeddings
   - Cấu hình các tham số như số lượng kết quả trả về...

4. **Node "Embeddings Mistral Cloud" (embeddingsMistralCloud)**
   - Thêm credentials Mistral Cloud API
   - Chọn model embeddings phù hợp

5. **Node "Google Drive(brand related data for chatbot)" (googleDrive)**
   - Thêm credentials Google Drive OAuth2
   - Chọn folder chứa tài liệu cần xử lý
   - Cấu hình các tham số như file types, max results...

6. **Node "Mistral Upload" (httpRequest)**
   - Thêm credentials Mistral Cloud API
   - Cấu hình endpoint upload file

7. **Node "Webhook" (webhook)**
   - Cấu hình path và HTTP method phù hợp
   - Đảm bảo webhook này được bảo mật

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Thêm một file mẫu vào Google Drive
   - Kích hoạt workflow bằng manual trigger
   - Kiểm tra quá trình xử lý và kết quả trong Qdrant

2. Bật Active workflow:
   - Sau khi test thành công, bật chế độ active
   - Kiểm tra lại các credentials và cấu hình

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi có câu hỏi mới
2. **Lưu log hoạt động**: Thêm node lưu log các câu hỏi và câu trả lời
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo hàng ngày về hoạt động chatbot
4. **Cải thiện OCR**: Thử nghiệm với các model OCR khác từ AWS Textract hoặc Google Vision

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình tạo chatbot hỗ trợ khách hàng với cơ sở kiến thức từ Google Drive. Bằng cách tích hợp OCR thông minh, trí tuệ nhân tạo và cơ sở dữ liệu vector, các sếp có thể cung cấp các câu trả lời chính xác và liên tục 24/7 cho khách hàng. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tiết kiệm thời gian xử lý tài liệu!