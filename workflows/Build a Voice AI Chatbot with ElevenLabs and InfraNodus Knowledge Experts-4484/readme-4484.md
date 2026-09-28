---
title: "🤖 Tạo Chatbot Trí Tuệ Nhân Tạo Voice AI với ElevenLabs & N8n: Hỗ Trợ Khách Hàng & Tăng Cường Trải Nghiệm Khách Hàng"
description: "Tự động hóa chatbot voice AI thông minh kết hợp ElevenLabs và n8n để trả lời câu hỏi khách hàng, tổng hợp kiến thức từ các nguồn chuyên môn (sách, bài viết) và cung cấp phản hồi cá nhân hóa 24/7. Giảm thời gian hỗ trợ, tăng trải nghiệm khách hàng và tối ưu hóa quy trình bán hàng."
slug: "chatbot-voice-ai-elevenlabs-n8n"
tags: [n8n, automation, ai-chatbot, elevenlabs, knowledge-graph, sales-support]
keywords: [chatbot voice ai n8n, tự động hóa hỗ trợ khách hàng, elevenlabs n8n workflow, chatbot trí tuệ nhân tạo, tự động hóa bán hàng, knowledge graph ai]
---

# 🚀 **Tạo Chatbot Trí Tuệ Nhân Tạo Voice AI với ElevenLabs & n8n: Hỗ Trợ Khách Hàng & Tăng Cường Trải Nghiệm Khách Hàng**

---

## **🎯 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, các doanh nghiệp thường phải gánh chịu những vấn đề sau khi hỗ trợ khách hàng thủ công:
- **Thời gian phản hồi chậm**: Đội ngũ hỗ trợ phải trả lời hàng trăm tin nhắn hàng ngày, dẫn đến trải nghiệm khách hàng không tốt.
- **Không thể hoạt động 24/7**: Khách hàng quốc tế hoặc khách hàng có nhu cầu hỗ trợ ngoài giờ làm việc bị bỏ lại một mình.
- **Không khai thác triệt để kiến thức nội bộ**: Các sách, bài viết, hoặc tài liệu chuyên môn trong doanh nghiệp thường nằm rải rác, khó truy cập và tổng hợp.
- **Phản hồi không cá nhân hóa**: Các câu trả lời chung chung không đáp ứng được nhu cầu cụ thể của từng khách hàng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo chatbot voice AI** sử dụng giọng nói tự nhiên (ElevenLabs) để tương tác với khách hàng qua Telegram, Slack, hoặc website.
✅ **Tích hợp kiến thức chuyên môn** từ các nguồn như sách, bài viết, hoặc đồ thị tri thức (InfraNodus) để trả lời chính xác và sâu sắc.
✅ **Hoạt động tự động 24/7** mà không cần can thiệp của con người.
✅ **Cá nhân hóa phản hồi** dựa trên lịch sử trò chuyện trước đó.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hỗ trợ**: Chatbot tự động trả lời 80% câu hỏi thường gặp, giảm tải cho đội ngũ hỗ trợ.
- **Trải nghiệm khách hàng cao cấp**: Khách hàng được tương tác qua giọng nói tự nhiên và phản hồi chính xác từ kiến thức chuyên môn.
- **Hoạt động liên tục**: Hỗ trợ khách hàng 24/7, không phụ thuộc vào giờ làm việc.
- **Tối ưu hóa bán hàng**: Khách hàng có thể được tư vấn sản phẩm chi tiết ngay lập tức, tăng tỷ lệ chuyển đổi.
- **Khai thác triệt để kiến thức nội bộ**: Tích hợp sách, bài viết, hoặc đồ thị tri thức để trả lời câu hỏi chuyên sâu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản ElevenLabs**:
   - Tạo tài khoản tại [elevenlabs.io](https://elevenlabs.io/) và lấy **API Key**.
   - Cài đặt **Conversational AI Agent** theo hướng dẫn dưới đây.
2. **Tài khoản InfraNodus** (nếu sử dụng đồ thị tri thức):
   - Tạo tài khoản tại [infranodus.com](https://infranodus.com/) và lấy **API Key** hoặc URL của đồ thị tri thức.
3. **Tài khoản OpenAI hoặc Google Gemini** (lựa chọn):
   - Đăng ký tại [OpenAI](https://openai.com/) hoặc [Google AI Studio](https://makersuite.google.com/) để lấy **API Key**.
4. **Nguồn kiến thức chuyên môn**:
   - Các sách, bài viết, hoặc đồ thị tri thức (InfraNodus) để chatbot tham khảo.
5. **N8n Self-hosted**:
   - Cài đặt n8n trên VPS hoặc máy chủ riêng để lưu trữ workflow.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link workflow gốc](https://n8n.io/workflows/4484) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán hoặc tải file JSON.
- **Không cần chỉnh sửa mã nguồn**, chỉ cần cấu hình các node như hướng dẫn dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **10 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node Webhook (Trigger)**
- **Tên node**: `Webhook`
- **Cấu hình**:
  - **Path**: Giá trị mặc định từ file JSON (ví dụ: `171bf9a6-1390-4195-bd6b-ff3df2e27d1c`).
  - **HTTP Method**: `POST`.
  - **Lưu ý**: Đây là **URL Webhook** sẽ được kết nối với **ElevenLabs Conversational AI Agent**. Các sếp **không cần thay đổi** giá trị này.

##### **🔹 Node AI Agent (Core Logic)**
- **Tên node**: `AI Agent` (type: `agent`).
- **Cấu hình**:
  - **System Prompt**: Các sếp cần **cập nhật mô tả các "Expert" (nguồn kiến thức)** trong phần `tools` của Agent. Ví dụ:
    ```
    You are an expert assistant who can consult multiple knowledge sources:
    1. Waves into Patterns Book Expert
    2. Special Agent's Manual Book Expert
    3. The Flow and the Notion Book
    4. The Polysingularity Letters Book
    When a user asks a question, choose the most relevant expert and ask them for help.
    ```
  - **Tools**: Các sếp cần **thêm mô tả chi tiết** cho mỗi "Expert" (node `httpRequestTool`) trong phần `Description` của tool. Ví dụ:
    ```
    Description: Expert on "Waves into Patterns" book by InfraNodus. Can answer questions about patterns, rhythms, and circadian cycles.
    ```

##### **🔹 Node Expert (HTTP Request Tools)**
Workflow này có **4 node `httpRequestTool`** đại diện cho các nguồn kiến thức (sách, bài viết). Các sếp cần:
- **Thay đổi `credentials`**:
  - Chọn `httpBearerAuth` và điền **API Key** của InfraNodus (nếu sử dụng).
  - Nếu không sử dụng InfraNodus, thay thế bằng **URL API** của nguồn kiến thức khác (ví dụ: API của Google Drive, Notion, hoặc cơ sở dữ liệu nội bộ).
- **Thay đổi `body.name`**:
  - Điền **tên đồ thị tri thức** (nếu sử dụng InfraNodus) hoặc **ID nguồn kiến thức** (nếu sử dụng nguồn khác).
  - Ví dụ:
    ```json
    {
      "name": "Waves into Patterns Book Expert",
      "url": "https://api.infranodus.com/graphs/{GRAPH_ID}",
      "method": "GET",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
    ```

##### **🔹 Node Chat Memory (Bảo lưu lịch sử trò chuyện)**
- **Tên node**: `Simple Memory` (type: `memoryBufferWindow`).
- **Cấu hình**:
  - **Window Size**: Đặt giá trị từ `1` đến `10` tùy thuộc vào số lượng tin nhắn cần lưu (ví dụ: `5` để lưu 5 tin nhắn gần nhất).
  - **Key**: Đặt tên khóa lưu trữ (ví dụ: `conversation_history`).

##### **🔹 Node LLM (OpenAI/Gemini)**
Workflow có **hai lựa chọn**:
1. **OpenAI (GPT-4o)**:
   - **Tên node**: `OpenAI Model` (type: `lmChatOpenAi`).
   - **Cấu hình**:
     - Chọn `openAiApi` trong `credentials` và điền **API Key**.
     - Đặt `model`: `gpt-4o`.
2. **Google Gemini**:
   - **Tên node**: `Google Gemini Chat Model` (type: `lmChatGoogleGemini`).
   - **Cấu hình**:
     - Chọn `googlePalmApi` trong `credentials` và điền **API Key**.

##### **🔹 Node Respond to Webhook**
- **Tên node**: `Respond to Webhook`.
- **Cấu hình**:
  - **Body**: Sử dụng kết quả từ `AI Agent` để trả lời khách hàng.
  - **Headers**: Đảm bảo `Content-Type: application/json`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và gửi một **dữ liệu mẫu** (ví dụ: `{"prompt": "Giải thích về chu kỳ sinh học trong sách Waves into Patterns", "sessionId": "abc123"}`).
   - Kiểm tra kết quả trong **n8n Logs** để đảm bảo workflow hoạt động.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với ElevenLabs Conversational AI**:
   - Theo hướng dẫn dưới đây để kết nối **Webhook** với **ElevenLabs Agent**:
     - Tạo **Agent** mới trong ElevenLabs với **System Prompt** như sau:
       ```
       You are well-versed on [tên nguồn kiến thức của bạn] through the tools you have access to.
       1) When you receive a user's message, first answer something like "I am consulting my knowledge and will respond soon."
       2) Then forward the user's message to the knowledge_base tool.
       3) When you receive a response from knowledge_base, use it to respond to the user, making it more concise but maintaining all specifics.
       ```
     - Thêm **Tool** mới với tên `knowledge_base` và URL Webhook từ n8n.
     - Thêm **Body Parameters**:
       - `prompt`: LLM prompt (dữ liệu từ user).
       - `sessionId`: `system__conversation_id` (để lưu lịch sử).
   - **Hướng dẫn chi tiết**: [ElevenLabs AI Voice Agent Setup](https://support.noduslabs.com/hc/en-us/articles/20318967066396).

2. **Tích hợp với Slack/Telegram**:
   - Sử dụng **node `slack`** hoặc **`telegram`** để gửi tin nhắn phản hồi từ chatbot về kênh Slack hoặc Telegram.
   - Ví dụ cấu hình cho Slack:
     ```json
     {
       "name": "Send to Slack",
       "type": "slack",
       "credentials": ["slackApi"],
       "keyParameters": {
         "channel": "#support",
         "text": "{{ $json.output.response }}"
       }
     }
     ```

3. **Lưu log và báo cáo**:
   - Thêm **node `googleSheets`** hoặc **`airtable`** để lưu lịch sử trò chuyện vào bảng tính hoặc cơ sở dữ liệu.
   - Ví dụ:
     ```json
     {
       "name": "Log to Google Sheets",
       "type": "googleSheets",
       "credentials": ["googleSheetsApi"],
       "keyParameters": {
         "sheetName": "Chatbot_Logs",
         "data": {
           "timestamp": "{{ $node["Webhook"].json["$.timestamp"] }}",
           "userMessage": "{{ $json.output.prompt }}",
           "botResponse": "{{ $json.output.response }}"
         }
       }
     }
     ```

4. **Cập nhật kiến thức định kỳ**:
   - Sử dụng **node `schedule`** để tự động cập nhật kiến thức từ các nguồn mới (ví dụ: cập nhật sách mới vào InfraNodus).

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tạo một chatbot voice AI thông minh**, tự động trả lời câu hỏi khách hàng từ kiến thức chuyên môn, và hoạt động 24/7 mà không cần can thiệp của con người. **Giảm thời gian hỗ trợ, tăng trải nghiệm khách hàng, và tối ưu hóa quy trình bán hàng** là những lợi ích mà các sếp sẽ nhận được khi áp dụng giải pháp này.

**Bắt đầu ngay hôm nay!**
1. Import workflow vào n8n.
2. Cấu hình các node theo hướng dẫn.
3. Kết nối với ElevenLabs và nguồn kiến thức của bạn.
4. Bật workflow và bắt đầu tự động hóa hỗ trợ khách hàng!

---
**🔗 [Xem video hướng dẫn chi tiết](https://www.youtube.com/watch?v=07-HZZQs5h0)** | **📖 [Tài liệu chính thức](https://support.noduslabs.com/hc/en-us/articles/20318967066396)**