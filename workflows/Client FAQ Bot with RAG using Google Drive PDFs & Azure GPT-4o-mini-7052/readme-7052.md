---
title: "🤖 Xây Dựng Chatbot FAQ Thông Minh Với RAG, GPT-4o-mini & Google Drive"
description: "Hướng dẫn chi tiết cách tạo Chatbot hỗ trợ khách hàng tự động trả lời dựa trên tài liệu PDF trong Google Drive, sử dụng n8n, Azure GPT-4o-mini và kỹ thuật RAG."
slug: "chatbot-faq-rag-google-drive-gpt-4o-mini"
tags: [n8n, automation, ai, rag, chatbot, azure-openai]
keywords: [n8n workflow, chatbot faq, rag google drive, azure gpt-4o-mini, tự động hóa hỗ trợ khách hàng]
---

# 🤖 Xây Dựng Chatbot FAQ Thông Minh Với RAG, GPT-4o-mini & Google Drive

Việc trả lời các câu hỏi lặp đi lặp lại của khách hàng (FAQ) đang ngốn mất hàng giờ mỗi ngày của đội ngũ hỗ trợ? Bạn có hàng tá tài liệu PDF, hướng dẫn sản phẩm nằm rải rác trong Google Drive nhưng không có cách nào để AI "đọc" và trả lời chính xác dựa trên nội dung đó?

Workflow này chính là giải pháp "chốt hạ" cho vấn đề đó. Chúng ta sẽ xây dựng một **AI Agent** sử dụng kỹ thuật **RAG (Retrieval-Augmented Generation)** để:
1. Nhận câu hỏi từ Webhook.
2. Tự động tìm kiếm và tải xuống các file PDF liên quan từ Google Drive.
3. Trích xuất nội dung văn bản từ PDF.
4. Sử dụng **Azure GPT-4o-mini** (mạnh mẽ, nhanh và tiết kiệm chi phí) để tổng hợp câu trả lời chính xác dựa trên dữ liệu thực tế, tránh tình trạng "bịa chuyện" (hallucination) của LLM thông thường.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chính xác tuyệt đối:** AI chỉ trả lời dựa trên nội dung trong file PDF của bạn, không bịa đặt thông tin.
- **Tiết kiệm chi phí:** Sử dụng GPT-4o-mini, một trong những model có hiệu suất/chi phí tốt nhất hiện nay.
- **Dễ dàng cập nhật:** Chỉ cần thêm file PDF mới vào Google Drive, chatbot sẽ tự động "học" được kiến thức mới mà không cần code lại.
- **Tích hợp linh hoạt:** Nhận câu hỏi qua Webhook, có thể kết nối với website, Slack, Telegram hoặc Discord.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2. **Tài khoản Google Drive:** Chứa các file PDF (FAQ, tài liệu sản phẩm, chính sách...).
3. **Tài khoản Azure OpenAI:**
   - Tạo Resource Group.
   - Deploy model `gpt-4o-mini`.
   - Lấy `Endpoint`, `API Key`, và `Deployment Name`.
4. **File JSON Workflow:** Từ link gốc hoặc file đính kèm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/7052` HOẶC chọn **Import from File** và upload file JSON.
3. Workflow sẽ hiển thị với 10 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình credentials/tham số:

**A. Node: `Webhook`**
- Đây là điểm đầu vào. Mặc định nó sẽ tạo ra một URL (ví dụ: `https://your-n8n.com/webhook/faq-bot`).
- Các sếp có thể giữ nguyên hoặc đổi Path nếu muốn.
- **Lưu ý:** Khi test, hãy dùng nút "Listen for test event" hoặc gửi request POST tới URL này với body JSON: `{ "question": "Câu hỏi của bạn" }`.

**B. Node: `Search files and folders` (Google Drive)**
- **Credentials:** Chọn tài khoản Google Drive đã kết nối.
- **Operation:** Search.
- **Query:** Đây là phần "thần thánh". Workflow sẽ dùng câu hỏi từ Webhook để tìm file.
  - *Mẹo:* Hãy đảm bảo tên file PDF trong Drive có chứa từ khóa liên quan đến nội dung (ví dụ: `FAQ-Van-Phong.pdf`, `Chinh-Sach-Bao-Hanh.pdf`).
  - Nếu muốn tìm tất cả file PDF, có thể chỉnh query thành `mimeType=application/pdf`.

**C. Node: `Download File` (Google Drive)**
- **Credentials:** Cùng tài khoản Google Drive ở trên.
- **Operation:** Download.
- Node này sẽ tự động lấy ID file từ bước tìm kiếm và tải về dạng Binary data.

**D. Node: `Extract from File`**
- **Operation:** Extract Text.
- **File Type:** PDF.
- Node này sẽ chuyển đổi file PDF thành văn bản thuần túy (plain text) để LLM có thể đọc được.

**E. Node: `Loop Over Items` (Split In Batches)**
- Node này giúp xử lý từng file một nếu có nhiều file được tìm thấy.
- Mặc định batch size là 1. Các sếp có thể tăng lên nếu muốn xử lý song song (nhưng cẩn thận rate limit của Azure).

**F. Node: `Azure OpenAI Chat Model`**
- **Credentials:** Chọn hoặc tạo mới Azure OpenAI credential.
  - **Azure OpenAI Endpoint:** Ví dụ: `https://your-resource-name.openai.azure.com/`
  - **API Key:** Dán API Key của bạn.
  - **Deployment Name:** Tên deployment của model `gpt-4o-mini` (ví dụ: `gpt-4o-mini-deploy`).
- **Model:** Chọn `gpt-4o-mini`.
- **Temperature:** Để `0.2` hoặc `0.3` để đảm bảo câu trả lời trung thực, ít sáng tạo bừa bãi.

**G. Node: `Basic LLM Chain`**
- **Prompt:** Đây là nơi các sếp "lập trình" cho AI.
  - Mặc định workflow đã có prompt mẫu. Các sếp nên chỉnh sửa phần **System Message** để định hình vai trò của bot.
  - *Ví dụ Prompt System:*
    ```text
    Bạn là một trợ lý hỗ trợ khách hàng thân thiện.
    Hãy trả lời câu hỏi dựa CHỈ VÀO nội dung trong tài liệu được cung cấp bên dưới.
    Nếu không tìm thấy thông tin trong tài liệu, hãy trả lời: "Xin lỗi, tôi chưa tìm thấy thông tin này trong tài liệu. Vui lòng liên hệ bộ phận hỗ trợ."
    Nội dung tài liệu:
    {{ $json.text }}
    ```
  - **User Message:** `{{ $json.question }}` (Lấy câu hỏi từ Webhook).

**H. Node: `Edit Fields` & `Edit Fields1`**
- Các node này dùng để làm sạch dữ liệu, chuẩn bị input cho LLM và output cho Webhook.
- Kiểm tra đảm bảo các mapping field đúng (ví dụ: lấy `text` từ Extract File, lấy `question` từ Webhook).

**I. Node: `Return Answer` (Respond to Webhook)**
- **Response Body:** Chọn `JSON`.
- **Value:** `{{ $json.text }}` (Câu trả lời từ LLM Chain).
- Node này sẽ gửi câu trả lời trở lại cho client (website/app) đã gọi Webhook.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Click vào node `Webhook` -> **Listen for test event**.
   - Mở Postman hoặc trình duyệt, gửi request POST tới URL Webhook với body:
     ```json
     {
       "question": "Chính sách đổi trả hàng là gì?"
     }
     ```
   - Quan sát workflow chạy qua các node: Tìm file -> Tải file -> Trích xuất -> LLM -> Trả lời.
   - Kiểm tra câu trả lời có chính xác không.
2. **Bật Active:**
   - Sau khi test thành công, tắt chế độ test.
   - Bật công tắc **Active** ở góc trên bên phải n8n.
   - Copy URL Webhook Production để tích hợp vào website hoặc ứng dụng của bạn.

### ✍️ Mẹo & gợi ý nâng cao

1. **Tối ưu hóa tên file PDF:**
   - RAG hoạt động dựa trên việc tìm kiếm file. Hãy đặt tên file PDF rõ ràng, chứa từ khóa (ví dụ: `FAQ-Thanh-Toan.pdf` thay vì `Doc1.pdf`). Điều này giúp node `Search files` tìm đúng file nhanh hơn.

2. **Phân tách tài liệu lớn:**
   - Nếu một file PDF quá dài (hàng trăm trang), LLM có thể bị quá tải context window. Hãy cân nhắc tách tài liệu thành các file nhỏ hơn theo chủ đề.

3. **Kết nối với Telegram/Slack:**
   - Thay vì dùng Webhook, các sếp có thể thay node `Webhook` bằng node `Telegram Trigger` hoặc `Slack Trigger` để biến nó thành bot chat trực tiếp.
   - Thay node `Return Answer` bằng node `Telegram` hoặc `Slack` để gửi tin nhắn.

4. **Lưu log câu hỏi:**
   - Thêm node `Google Sheets` hoặc `Postgres` sau node `Webhook` để lưu lại tất cả các câu hỏi khách hàng đã hỏi. Điều này giúp các sếp biết khách hàng quan tâm điều gì nhất và cải thiện tài liệu FAQ.

5. **Thêm bước xác thực:**
   - Nếu muốn bảo mật, thêm node `IF` hoặc `Verify Token` trước khi xử lý để chỉ cho phép các request hợp lệ.

### 📌 Kết luận

Với workflow này, các sếp đã sở hữu một **Chatbot FAQ thông minh**, chính xác và tiết kiệm chi phí. Thay vì trả lời thủ công, AI sẽ làm việc 24/7, dựa trên chính tài liệu của công ty bạn.

Hãy bắt đầu ngay hôm nay:
1. Import workflow.
2. Kết nối Google Drive và Azure OpenAI.
3. Thử hỏi một câu hỏi và xem AI trả lời thế nào.

Chúc các sếp triển khai thành công và tự động hóa hiệu quả! 🚀

:::note[Hỗ trợ]
Nếu gặp lỗi khi kết nối Azure OpenAI, hãy kiểm tra kỹ:
- Endpoint có dấu `/` ở cuối không?
- Deployment Name có đúng không?
- API Key có bị hết hạn không?
:::