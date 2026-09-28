---
title: "🤖 Tạo Bot Trả Lời Thông Minh Telegram với Google Gemini & Supabase – Tự Động Hóa Hỗ Trợ Khách Hàng 24/7"
description: "Workflow này tự động hóa việc xây dựng một bot Telegram thông minh sử dụng Google Gemini (AI) kết hợp với cơ sở dữ liệu Supabase để trả lời FAQ khách hàng một cách cá nhân hóa và tự động. Giúp tiết kiệm thời gian hỗ trợ, cải thiện trải nghiệm người dùng và hoạt động liên tục mà không cần code."
slug: "tao-bot-traloi-thong-minh-telegram-google-gemini-supabase"
tags: [n8n, automation, ai-chatbot, telegram-bot, google-gemini, supabase, no-code]
keywords: [n8n workflow telegram bot, tự động hóa hỗ trợ khách hàng, google gemini n8n, bot trả lời tự động telegram, supabase n8n, chatbot ai không cần code]
---

# 🚀 **Tạo Bot Trả Lời Thông Minh Telegram với Google Gemini & Supabase**

## **Giới Thiệu**
Hiện nay, việc hỗ trợ khách hàng thông qua Telegram đang trở thành một trong những kênh quan trọng nhất cho doanh nghiệp. Tuy nhiên, phải mất nhiều thời gian để trả lời các câu hỏi thường gặp (FAQ) một cách thủ công. **Workflow này giúp các sếp tự động hóa hoàn toàn quá trình này bằng một bot Telegram thông minh, kết hợp AI Google Gemini và cơ sở dữ liệu Supabase**, để:
- **Trả lời tự động** cho khách hàng với độ chính xác cao.
- **Cá nhân hóa** trải nghiệm người dùng bằng cách lưu lịch sử tương tác.
- **Hoạt động 24/7** mà không cần can thiệp của nhân viên.
- **Tiết kiệm thời gian** cho đội ngũ hỗ trợ, tập trung vào các vấn đề phức tạp hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên một VPS chuyên dụng để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% hỗ trợ FAQ**: Khách hàng nhận câu trả lời ngay lập tức, không cần chờ đợi.
- **Cá nhân hóa tương tác**: Bot nhớ lịch sử người dùng và trả lời phù hợp với từng cá nhân.
- **Tiết kiệm chi phí nhân sự**: Giảm thiểu thời gian của đội ngũ hỗ trợ cho các câu hỏi đơn giản.
- **Hiệu suất cao**: AI Google Gemini phân tích và trả lời nhanh chóng, chính xác hơn so với con người.
- **Dễ dàng mở rộng**: Có thể thêm nhiều FAQ hoặc tích hợp với các dịch vụ khác (Slack, Email, CRM).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot Telegram thông qua [@BotFather](https://t.me/BotFather) và lấy **API Key**.
   - Cài đặt bot vào nhóm hoặc cá nhân để người dùng có thể tương tác.

2. **Supabase Database**:
   - Tạo một cơ sở dữ liệu trên [Supabase](https://supabase.com/) và tạo bảng `users` với các trường:
     - `id` (UUID)
     - `telegram_id` (ID của người dùng Telegram)
     - `created_at` (thời gian tạo)
   - Lấy **Supabase API Key** và **Project URL** từ Dashboard Supabase.

3. **Google Gemini API**:
   - Đăng ký API Key từ [Google AI Studio](https://aistudio.google/) và chọn mô hình **Gemini Pro**.

4. **N8n Workflow**:
   - N8n phiên bản mới nhất (cần cài đặt node `@n8n/n8n-nodes-langchain` để hỗ trợ Google Gemini).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9762](https://n8n.io/workflows/9762) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON đã tải về.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **9 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu hình Telegram Trigger**
- Node: **Telegram Trigger**
  - Chọn **credentials**: `telegramApi` (đã tạo từ bước 1).
  - Thiết lập **Webhook URL**: `https://<your-n8n-domain>/telegramTrigger/<bot-token>` (thay `<your-n8n-domain>` bằng domain hoặc IP của VPS n8n).
  - **Lưu ý**: Nếu self-host, cần mở port 443 (HTTPS) hoặc 80 (HTTP) trên VPS.

##### **B. Cấu hình Supabase**
- Node: **Check if User Exists in Supabase**
  - Chọn **credentials**: `supabaseApi`.
  - Điền **Project URL** và **API Key** từ Supabase.
  - Thiết lập **Query**:
    ```sql
    SELECT * FROM users WHERE telegram_id = $telegram_id
    ```
    (Tham số `$telegram_id` sẽ được truyền tự động từ Telegram Trigger).

- Node: **Save New User to Supabase**
  - Chọn **credentials**: `supabaseApi`.
  - Thiết lập **Query**:
    ```sql
    INSERT INTO users (telegram_id, created_at) VALUES ($telegram_id, NOW())
    ```
    (Tham số `$telegram_id` sẽ được truyền từ Telegram Trigger).

##### **C. Cấu hình Google Gemini**
- Node: **Google Gemini Chat Model**
  - Chọn **credentials**: `googleGeminiApi` (tạo mới trong n8n).
  - Điền **API Key** từ Google AI Studio.
  - Thiết lập **Prompt** (ví dụ):
    ```
    You are a helpful FAQ assistant. Answer the user's question based on the following FAQ context:
    $faq_context
    Question: $question
    Answer:
    ```

- Node: **Load FAQ Context for AI**
  - Node này **set** biến `$faq_context` chứa nội dung FAQ (các sếp có thể tự thêm vào bằng cách chỉnh sửa node **Set** này).
  - Ví dụ:
    ```json
    {
      "faq_context": "1. Câu hỏi thường gặp 1: Trả lời 1.\n2. Câu hỏi thường gặp 2: Trả lời 2."
    }
    ```

##### **D. Cấu hình Telegram Bot trả lời**
- Node: **Send Welcome Message (New User)**
  - Chọn **credentials**: `telegramApi`.
  - Thiết lập **Message**:
    ```
    Xin chào! Tôi là bot hỗ trợ của [Tên Doanh Nghiệp]. Hãy gửi câu hỏi của bạn để tôi giúp đỡ!
    ```

- Node: **Send AI Answer to User**
  - Chọn **credentials**: `telegramApi`.
  - Thiết lập **Message**:
    ```
    $json["response"]
    ```
    (Tham số `$json["response"]` sẽ chứa câu trả lời từ Google Gemini).

##### **E. Cấu hình Node "If" (Route: New or Existing User?)**
- Node này **kiểm tra** xem người dùng có tồn tại trong Supabase không.
- Nếu **không tồn tại** → Thực hiện **Save New User** và **Send Welcome Message**.
- Nếu **tồn tại** → Bỏ qua và chuyển sang **Process Question with Gemini**.

##### **F. Cấu hình Node Agent (Process Question with Gemini)**
- Node: **Process Question with Gemini**
  - Chọn **credentials**: `googleGeminiApi`.
  - Thiết lập **Agent Configuration**:
    - **Model**: `gemini-pro`.
    - **Tools**: Chọn **LangChain Tools** (nếu cần).
    - **Prompt**: Sử dụng biến `$question` từ Telegram Trigger và `$faq_context` từ node **Set**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một tin nhắn từ Telegram Bot đến bot của mình (ví dụ: `/start` hoặc một câu hỏi mẫu).
   - Kiểm tra **n8n Editor** để xem workflow có chạy đúng không và trả lời như mong đợi.

2. **Bật Active Workflow**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Email**:
   - Sử dụng node **Slack** hoặc **Email** để gửi báo cáo hoặc thông báo khi có câu hỏi mới.

2. **Lưu log tương tác**:
   - Thêm node **StickyNote** hoặc **Database** để lưu lịch sử câu hỏi và trả lời của người dùng.

3. **Cập nhật FAQ tự động**:
   - Sử dụng node **HTTP Request** để lấy FAQ từ một file JSON hoặc Google Sheets và tự động cập nhật `$faq_context`.

4. **Thêm tính năng chat history**:
   - Sử dụng **Supabase** để lưu lịch sử chat của từng người dùng và trả lời dựa trên lịch sử đó.

5. **Tích hợp với CRM**:
   - Nếu khách hàng là khách hàng đã có trong hệ thống, bạn có thể kết nối với **Zapier** hoặc **Make (Integromat)** để lấy thông tin chi tiết và trả lời cá nhân hóa hơn.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa hỗ trợ khách hàng thông qua Telegram một cách thông minh và hiệu quả. Với **Google Gemini**, bot không chỉ trả lời nhanh chóng mà còn **hiểu ngữ cảnh** và **cá nhân hóa** trải nghiệm người dùng. **Không cần code**, chỉ cần cấu hình vài bước là có thể triển khai ngay!

**Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ hỗ trợ của mình!** 🚀

---
**🔹 Cần hỗ trợ thêm?**
- Trả lời câu hỏi trong [n8n Community](https://community.n8n.io/).
- Liên hệ với tác giả [Mohammad Jibril](https://n8n.io/workflows/9762) để có thêm hướng dẫn chi tiết.