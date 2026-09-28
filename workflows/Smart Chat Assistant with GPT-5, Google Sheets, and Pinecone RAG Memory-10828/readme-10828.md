---
title: "🤖 Trợ lý Chat thông minh với GPT-5, Google Sheets và Pinecone RAG Memory"
description: "Tự động hóa hoàn toàn quá trình chatbot với trí nhớ dài hạn, truy xuất ngữ cảnh từ Pinecone và Google Sheets, và ghi log cuộc trò chuyện."
slug: "tro-ly-chat-thong-minh-voi-gpt-5-google-sheets-pinecone-rag-memory"
tags: [n8n, automation, no-code, chatbot, ai, rag, pinecone, google-sheets]
keywords: [n8n workflow, tự động hóa chatbot, trí nhớ dài hạn, pinecone, google sheets, gpt-5]
---

# 🤖 Trợ lý Chat thông minh với GPT-5, Google Sheets và Pinecone RAG Memory

[Các sếp] có bao giờ phải tự trả lời hàng trăm tin nhắn khách hàng mỗi ngày không? Hay phải tìm kiếm thông tin liên tục trong các tài liệu để trả lời câu hỏi của khách hàng? Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình này với một trợ lý chat thông minh có trí nhớ dài hạn, khả năng truy xuất ngữ cảnh từ Pinecone và Google Sheets, và tự động ghi log tất cả cuộc trò chuyện.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động trả lời khách hàng 24/7 mà không cần can thiệp.
- **Chính xác cao**: Truy xuất thông tin từ cả dữ liệu cấu trúc (Google Sheets) và ngữ nghĩa (Pinecone).
- **Trí nhớ dài hạn**: Ghi nhớ ngữ cảnh cuộc trò chuyện để trả lời chính xác hơn.
- **Dễ dàng quản lý**: Tất cả cuộc trò chuyện được tự động ghi log vào Google Sheets.
- **Tự động hóa hoàn toàn**: Không cần viết code, chỉ cần cấu hình các tài khoản và API keys.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng GPT-5).
- Tài khoản Google Sheets OAuth2 (để lưu trữ và truy xuất dữ liệu).
- Tài khoản Pinecone API (để lưu trữ và truy xuất ngữ cảnh).
- Tài khoản Google Drive OAuth2 (để theo dõi và tải lên các tài liệu mới).
- Tài khoản Gmail OAuth2 (để gửi email báo cáo hàng tuần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/10828](https://n8n.io/workflows/10828).
2. Click vào nút "Import" để tải xuống file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When chat message received"**:
   - Cấu hình webhook để nhận tin nhắn từ khách hàng.
   - Lưu ý: URL webhook sẽ được tạo tự động khi kích hoạt node này.

2. **Node "OpenAI Chat Model"**:
   - Chọn credentials "openAiApi".
   - Chọn model GPT-5 (hoặc model tương đương mới nhất).

3. **Node "Google Drive Trigger"**:
   - Chọn credentials "googleDriveOAuth2Api".
   - Cấu hình để theo dõi thư mục chứa các tài liệu mới.

4. **Node "Get Previous Content from Sheet" và "Conversation Logging"**:
   - Chọn credentials "googleSheetsOAuth2Api".
   - Cập nhật "Document ID" để trỏ đến Google Sheet lưu trữ cuộc trò chuyện.
   - Đảm bảo Sheet có các cột: Timestamp, User Input, Detected Intent, AI Response.

5. **Node "Pinecone Vector Store Insert" và "Pinecone Vector Store Query for Knowledge Base"**:
   - Chọn credentials "pineconeApi".
   - Thay thế "whatsappchatbot" bằng tên index của bạn trong Pinecone.

6. **Node "Send Chat History with attachment"**:
   - Chọn credentials "gmailOAuth2".
   - Cấu hình địa chỉ email nhận báo cáo hàng tuần.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một tin nhắn thử nghiệm vào webhook.
   - Kiểm tra xem dữ liệu có được ghi log vào Google Sheets và Pinecone không.
2. Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thay thế node Gmail bằng node Slack/Telegram để gửi báo cáo.
- **Lưu log nâng cao**: Thêm các thông tin như tên khách hàng, ID phiên chat vào Google Sheets.
- **Tự động hóa nâng cao**: Kết hợp với các node khác để tự động hóa các quy trình khác như gửi email tự động, cập nhật CRM...
- **Tối ưu hóa chi phí**: Sử dụng các model OpenAI rẻ hơn (như GPT-3.5 Turbo) cho các cuộc trò chuyện không yêu cầu ngữ cảnh phức tạp.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình chatbot với trí nhớ dài hạn, truy xuất ngữ cảnh từ Pinecone và Google Sheets, và ghi log tất cả cuộc trò chuyện. Với các bước cấu hình đơn giản và không cần viết code, các sếp có thể triển khai ngay lập tức và tiết kiệm thời gian quý giá. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tối ưu hóa quy trình làm việc!