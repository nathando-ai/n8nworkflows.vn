---
title: "🤖 Slack AI Chatbot với RAG, Claude 3.7 Sonnet và Google Drive - Tự động hóa 100% không cần code"
description: "Hướng dẫn chi tiết cách tạo Slack AI Chatbot tích hợp RAG, Claude 3.7 Sonnet và Google Drive để tự động hóa các tác vụ lặp lại trong nhóm làm việc"
slug: "slack-ai-chatbot-voi-rag-claude-3-7-sonnet-google-drive"
tags: [n8n, automation, no-code, ai, slack, google-drive, qdrant]
keywords: [n8n workflow, tự động hóa, chatbot slack, claude 3.7 sonnet, google drive, qdrant]
---

# 🤖 Slack AI Chatbot với RAG, Claude 3.7 Sonnet và Google Drive - Tự động hóa 100% không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ cảm thấy mệt mỏi khi phải trả lời liên tục các câu hỏi lặp lại từ đồng nghiệp về chính sách công ty, yêu cầu IT, hoặc thông tin về ngày nghỉ? Với Slack AI Chatbot này, các sếp có thể tự động hóa hoàn toàn quá trình này, giúp nhóm làm việc của mình hiệu quả hơn bao giờ hết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian cho các sếp: Không cần phải trả lời các câu hỏi lặp lại
- Tăng hiệu suất làm việc: Đồng nghiệp có thể nhận được thông tin ngay lập tức 24/7
- Tăng tính cá nhân hóa: Chatbot có thể cung cấp thông tin phù hợp với từng người dùng
- Giảm tải công việc: Các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền quản trị
- Tài khoản Google Drive với các tài liệu cần chia sẻ
- API Key từ OpenAI (cho embeddings)
- API Key từ Anthropic (cho Claude 3.7 Sonnet)
- Tài khoản Qdrant (cho vector database)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/3414](https://n8n.io/workflows/3414)
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get message" (slackTrigger)**:
   - Cấu hình credentials Slack API
   - Đảm bảo bot đã được thêm vào channel Slack với các scope cần thiết

2. **Node "Create collection" (httpRequest)**:
   - Thay đổi QDRANTURL và COLLECTION trong body request
   - Cấu hình credentials HTTP Header Auth

3. **Node "Get folder" (googleDrive)**:
   - Cấu hình credentials Google Drive OAuth2 API
   - Chọn folder chứa các tài liệu cần chia sẻ

4. **Node "Embeddings OpenAI1" (embeddingsOpenAi)**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo có đủ credit để sử dụng embeddings

5. **Node "Anthropic Chat Model" (lmChatAnthropic)**:
   - Cấu hình credentials Anthropic API
   - Đảm bảo đã chọn model "claude-3-7-sonnet-20250219"

6. **Node "RAG" (vectorStoreQdrant)**:
   - Cấu hình credentials Qdrant API
   - Thay đổi QDRANTURL và COLLECTION

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng node "When clicking ‘Test workflow’"
2. Kiểm tra kết quả trên Slack channel
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack Notifications để nhận thông báo khi có câu hỏi mới
- Thêm node lưu log các câu hỏi và câu trả lời để phân tích sau này
- Tích hợp với Google Calendar để tự động trả lời về lịch làm việc
- Sử dụng node "Send message" để gửi báo cáo định kỳ về hoạt động của chatbot

### 📌 Kết luận
Slack AI Chatbot với RAG, Claude 3.7 Sonnet và Google Drive là giải pháp hoàn hảo cho các sếp muốn tự động hóa các tác vụ lặp lại trong nhóm làm việc. Với workflow này, các sếp có thể tiết kiệm thời gian, tăng hiệu suất làm việc và cung cấp dịch vụ hỗ trợ tốt hơn cho đồng nghiệp. Hãy áp dụng ngay để trải nghiệm sự khác biệt!