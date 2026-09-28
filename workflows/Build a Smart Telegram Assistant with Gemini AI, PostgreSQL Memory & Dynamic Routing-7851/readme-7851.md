---
title: "🤖 Tự Động Hóa Trợ Lý Telegram Thông Minh Với Gemini AI, Bộ Nhớ PostgreSQL & Động Lực Hướng Điểm"
description: "Xây dựng trợ lý Telegram AI thông minh tự động hóa tương tác, nhớ lịch sử chat, phân loại và xử lý yêu cầu với Gemini AI, PostgreSQL và động lực hướng điểm. Giảm chi phí, tăng tốc độ phản hồi và tối ưu hóa trải nghiệm người dùng."
slug: "tay-dong-hoa-tro-ly-telegram-thong-minh-gemini-ai-postgresql"
tags: [n8n, automation, ai-chatbot, gemini-ai, postgresql, telegram-bot, no-code, llm]
keywords: [n8n workflow telegram ai, tự động hóa trợ lý telegram, gemini ai postgresql, động lực hướng điểm, chatbot thông minh, giảm chi phí llm]
---

# 🚀 **Tự Động Hóa Trợ Lý Telegram Thông Minh Với Gemini AI, PostgreSQL & Động Lực Hướng Điểm**

## **Giới Thiệu**
Các sếp đang gặp khó khăn khi phải tương tác với khách hàng qua Telegram một cách thủ công, mất thời gian ghi nhớ lịch sử chat, hoặc không thể xử lý yêu cầu phức tạp một cách hiệu quả? **Workflow này giải quyết tất cả những vấn đề đó bằng cách tự động hóa một trợ lý Telegram AI thông minh**, tích hợp:
- **Gemini AI** (Google) để xử lý yêu cầu với độ chính xác cao và động lực hướng điểm (model selector).
- **PostgreSQL** để lưu trữ và nhớ lịch sử chat, tối ưu hóa trải nghiệm người dùng.
- **Động lực hướng điểm** (difficulty-based routing) để chọn model phù hợp (Flash Lite, Flash, Pro) dựa trên độ phức tạp của yêu cầu, giảm chi phí và tăng tốc độ phản hồi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí LLM**: Sử dụng model Gemini 2.5 Flash Lite cho yêu cầu đơn giản, chỉ sử dụng Pro khi cần thiết.
- **Tốc độ phản hồi nhanh**: Động lực hướng điểm và tối ưu hóa bộ nhớ PostgreSQL làm giảm thời gian xử lý.
- **Nhớ lịch sử chat**: PostgreSQL lưu trữ toàn bộ lịch sử tương tác, giúp trợ lý "nhớ" từng cuộc trò chuyện trước đó.
- **Xử lý đa phương thức**: Hỗ trợ văn bản, âm thanh, và hình ảnh (có thể mở rộng).
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động 24/7.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy `API Token`.
2. **API Key Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và lấy `API Key`.
3. **PostgreSQL Database**:
   - Cài đặt PostgreSQL (cục bộ hoặc cloud) và tạo một database mới.
   - Cung cấp `host`, `port`, `database name`, `username`, và `password`.
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS hoặc máy chủ riêng (không dùng phiên bản cloud miễn phí).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7851](https://n8n.io/workflows/7851) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
- **Không quên chọn "Import as new workflow"** để tránh lỗi cấu hình.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **25 node** phức tạp, các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu hình Credentials**
- **Telegram API**:
  - Node: `Telegram Trigger`, `Send a text message`, `Typing…`, `Download Voice Message`.
  - Điền `API Token` từ bot Telegram vào `telegramApi` trong **Credentials Management**.

- **Google Palm API**:
  - Node: `Gemini 2.5 Flash Lite`, `Gemini 2.5 Flash`, `Gemini 2.5 Pro`, `Analyze voice message`, `Summarize & Categorize`.
  - Điền `API Key` từ Google AI Studio vào `googlePalmApi`.

- **PostgreSQL**:
  - Node: `Get Chat Memory`, `Create Chat Memory Table`, `Update Chat Memory (User and Agent)`.
  - Cấu hình:
    - `Host`: `localhost` (hoặc IP VPS).
    - `Port`: `5432` (mặc định).
    - `Database`: Tên database bạn tạo.
    - `Username` & `Password`: Thông tin đăng nhập.

##### **B. Cấu hình Node Quá Trình**
1. **`Create Chat Memory Table` (PostgreSQL)**:
   - Chạy node này **một lần duy nhất** để tạo bảng `chat_memory` với cấu trúc:
     ```sql
     CREATE TABLE chat_memory (
       id SERIAL PRIMARY KEY,
       session_id VARCHAR(255),
       user_message TEXT,
       agent_message TEXT,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
     );
     ```
   - **Lưu ý**: Nếu bảng đã tồn tại, bỏ qua node này.

2. **`Model Selector`**:
   - Node này **động lực hướng điểm** (difficulty-based) để chọn model Gemini phù hợp:
     - **Difficulty 1** → `Gemini 2.5 Flash Lite` (rẻ, nhanh).
     - **Difficulty 2** → `Gemini 2.5 Flash`.
     - **Difficulty 3** → `Gemini 2.5 Pro` (đắt, phức tạp).
   - **Cấu hình**:
     - Đảm bảo node `Summarize & Categorize` trả về `difficulty` trong JSON output (ví dụ: `{"difficulty": 1}`).

3. **`Summarize & Categorize` (Chain LLM)**:
   - Node này **tóm tắt lịch sử chat** và phân loại độ phức tạp.
   - **Prompt mẫu** (có thể tùy chỉnh):
     ```
     Tóm tắt lịch sử chat này và phân loại độ phức tạp (1-3) của yêu cầu mới:
     - Lịch sử: [Lịch sử chat từ PostgreSQL]
     - Yêu cầu mới: [Yêu cầu của người dùng]
     Trả về JSON: {"summary": "...", "difficulty": 1}
     ```

4. **`Agent` (LangChain Agent)**:
   - Node này kết hợp:
     - Yêu cầu của người dùng.
     - Lịch sử chat đã tóm tắt.
     - Độ phức tạp (`difficulty`).
   - **Cấu hình**:
     - Đảm bảo `input` của node này là JSON hợp lệ (ví dụ: `{"query": "...", "context": "...", "difficulty": 1}`).

5. **`MarkdownV2` (Code Node)**:
   - Node này **chuyển đổi output của Gemini thành Markdown V2** để Telegram hiển thị đẹp.
   - **Mã mẫu** (có thể chỉnh sửa):
     ```javascript
     // Chuyển đổi text thành Markdown V2
     return {
       json: {
         text: `*Trợ lý:*\n${item.json.output.text}`,
         parse_mode: "MarkdownV2"
       }
     };
     ```

6. **`Update Chat Memory` (PostgreSQL)**:
   - Node này **cập nhật bảng `chat_memory`** với hai dòng (người dùng + trợ lý) để tối ưu hóa tốc độ.
   - **Query mẫu**:
     ```sql
     INSERT INTO chat_memory (session_id, user_message, agent_message)
     VALUES ($1, $2, $3);
     ```
   - **Lưu ý**: `session_id` phải trùng với `session_id` trong `Get Chat Memory`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một tin nhắn văn bản hoặc âm thanh đến bot Telegram.
   - Kiểm tra:
     - Bot có phản hồi không?
     - Lịch sử chat có được lưu trong PostgreSQL không?
     - Model được chọn có phù hợp với độ phức tạp không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Hỗ trợ hình ảnh/video**:
   - Sử dụng workflow mở rộng từ [n8n.io/workflows/7455](https://n8n.io/workflows/7455) để xử lý file đa phương thức.

2. **Gửi báo cáo định kỳ**:
   - Thêm node **Email** hoặc **Slack** để gửi báo cáo tổng hợp hoạt động của bot hàng ngày.

3. **Cập nhật model mới**:
   - Nếu Google ra model mới (ví dụ: Gemini 1.5), các sếp có thể thêm node mới và cập nhật `Model Selector`.

4. **Log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu log tất cả tương tác (giúp theo dõi và phân tích).

5. **Tối ưu hóa chi phí**:
   - Sử dụng **rate limiting** cho API Google để tránh bị chặn (thêm node `set` để giới hạn số lần gọi API/ngày).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa trợ lý Telegram AI, giảm chi phí, tăng hiệu suất và cải thiện trải nghiệm người dùng. Với **động lực hướng điểm**, **PostgreSQL** và **Gemini AI**, các sếp có thể xây dựng một bot thông minh, tự động hóa hoàn toàn và dễ dàng mở rộng.

**Hành động ngay!**
- Import workflow và bắt đầu tự động hóa ngay hôm nay.
- Tùy chỉnh prompt và model để phù hợp với ngành nghề của doanh nghiệp.
- Liên hệ với tác giả [John Silva](mailto:johnsilva11031@gmail.com) nếu cần hỗ trợ thêm!

---
**#n8n #Automation #AIChatbot #GeminiAI #PostgreSQL #TelegramBot**