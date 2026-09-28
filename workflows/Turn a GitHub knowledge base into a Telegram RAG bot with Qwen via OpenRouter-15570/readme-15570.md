---
title: "🤖 Chuyển đổi cơ sở kiến thức GitHub thành chatbot Telegram với Qwen qua OpenRouter"
description: "Hướng dẫn tự động hóa chuyển đổi cơ sở kiến thức từ GitHub thành chatbot Telegram sử dụng mô hình Qwen qua OpenRouter, không cần cơ sở dữ liệu vector hay embeddings."
slug: "chuyen-doi-github-telegram-rag-bot-qwen-openrouter"
tags: [n8n, automation, no-code, ai, telegram, github]
keywords: [n8n workflow, tự động hóa, chatbot, RAG, Qwen, OpenRouter]
---

# 🤖 Chuyển đổi cơ sở kiến thức GitHub thành chatbot Telegram với Qwen qua OpenRouter

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý kiến thức thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình truy xuất kiến thức từ GitHub
- Tiết kiệm thời gian và chi phí cho doanh nghiệp
- Cung cấp câu trả lời chính xác dựa trên kiến thức doanh nghiệp
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tích hợp dễ dàng với các hệ thống hiện có
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và token bot từ @BotFather
- GitHub Fine-grained Personal Access Token (chỉ có quyền đọc)
- Tài khoản OpenRouter (hoặc endpoint OpenAI-compatible)
- File kiến thức dạng JSON trên GitHub
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15570)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoặc copy nội dung JSON và chọn "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When Message Received" (telegramTrigger)**:
   - Thêm credentials Telegram Bot API
   - Đảm bảo bot đã được thêm vào nhóm/channel cần sử dụng

2. **Node "Fetch GitHub File" (github)**:
   - Cấu hình các tham số:
     - Owner: Tên tài khoản GitHub của bạn
     - Repository: Tên repository chứa file kiến thức
     - File Path: Đường dẫn đến file JSON (ví dụ: kb.json)
   - Thêm credentials GitHub API

3. **Node "OpenAI Qwen Model" (lmChatOpenAi)**:
   - Thêm credentials OpenRouter
   - Đảm bảo model "qwen/qwen3-235b-a22b-2507" có sẵn trong tài khoản OpenRouter

4. **Node "Send Telegram Message" (telegram)**:
   - Thêm credentials Telegram Bot API (cùng với node đầu tiên)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn "/ask [câu hỏi của bạn]" đến bot Telegram
   - Kiểm tra kết quả trả về từ workflow
2. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hóa truy xuất**:
   - Chỉnh sửa node "Perform Rough Match" để trả về 3 hoặc 5 chunk thay vì 2
   - Điều này sẽ cải thiện chất lượng câu trả lời nhưng tăng chi phí token

2. **Cập nhật tự động**:
   - Sửa đổi file kb.json trên GitHub
   - Workflow sẽ tự động lấy dữ liệu mới mỗi khi có yêu cầu

3. **Đa ngôn ngữ**:
   - Workflow hoạt động với bất kỳ ngôn ngữ nào trong cơ sở kiến thức
   - Mô hình sẽ trả lời bằng ngôn ngữ tương ứng với câu hỏi

4. **Kết nối đa nguồn**:
   - Kết hợp với các nguồn dữ liệu khác như Notion DB, Google Sheets

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để chuyển đổi cơ sở kiến thức từ GitHub thành chatbot Telegram với khả năng RAG (Retrieval-Augmented Generation). Với thiết kế đơn giản nhưng hiệu quả, nó giúp doanh nghiệp tự động hóa quá trình truy xuất kiến thức một cách chi phí thấp và dễ dàng bảo trì. Các sếp có thể dễ dàng triển khai và tùy chỉnh workflow này để phù hợp với nhu cầu cụ thể của doanh nghiệp.