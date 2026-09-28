---
title: "🤖 Chatbot CV Tự Động Hóa với AI Gemini + Pinecone: Tự Động Học Tập & Gửi Báo Cáo Email Hàng Ngày"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp xây dựng một chatbot CV thông minh, tự động cập nhật nội dung từ Google Drive, lưu trữ hội thoại trong vector database Pinecone, và gửi báo cáo tổng hợp email hàng ngày. Giúp tiết kiệm thời gian lên tới 80% trong việc tương tác với ứng viên."
slug: "chatbot-cv-ai-gemini-pinecone"
tags: [n8n, automation, ai, google-gemini, pinecone, no-code, chatbot, cv-automation, email-reporting]
keywords: [n8n workflow cv, tự động hóa chatbot cv, gemini ai n8n, pinecone vector database, báo cáo email tự động, tự động hóa tuyển dụng]
---

# 🚀 **Chatbot CV Tự Động Hóa với AI Gemini + Pinecone: Tự Học Tập & Gửi Báo Cáo Email Hàng Ngày**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, khi tuyển dụng, các sếp thường phải:
- **Tự trả lời hàng trăm câu hỏi về CV** một cách lặp đi lặp lại.
- **Lưu trữ và theo dõi hội thoại** một cách thủ công, dễ bị mất mát.
- **Không tự động cập nhật** khi CV được chỉnh sửa, dẫn đến thông tin lỗi thời.
- **Không có báo cáo tổng hợp** về các cuộc trò chuyện với ứng viên.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động học tập từ CV** khi được upload/ chỉnh sửa lên Google Drive.
✅ **Chatbot AI thông minh** trả lời dựa trên nội dung CV (sử dụng **Google Gemini** + **Pinecone Vector DB**).
✅ **Lưu trữ hội thoại** trong **NocoDB** (có thể thay thế bằng cơ sở dữ liệu khác).
✅ **Gửi báo cáo email tổng hợp** hàng ngày về tất cả các cuộc trò chuyện.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chatbot tự động trả lời thay vì các sếp phải làm thủ công.
- **Cập nhật tự động**: Khi CV được chỉnh sửa, chatbot sẽ tự động học tập và cập nhật kiến thức.
- **Hội thoại được lưu trữ**: Tất cả cuộc trò chuyện được ghi lại trong **NocoDB** (hoặc cơ sở dữ liệu khác).
- **Báo cáo email tự động**: Mỗi ngày, hệ thống sẽ gửi email tổng hợp tất cả cuộc trò chuyện.
- **Trải nghiệm cá nhân hóa**: Chatbot trả lời dựa trên **vector database**, không phải là câu trả lời cố định.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để sử dụng **Google Gemini API**).
2. **Tài khoản Pinecone** (để lưu trữ vector database).
3. **Tài khoản Google Drive** (để lưu CV và kích hoạt trigger tự động).
4. **Tài khoản Gmail** (để gửi báo cáo email hàng ngày).
5. **Tài khoản NocoDB** (để lưu trữ lịch sử hội thoại, *có thể thay thế bằng cơ sở dữ liệu khác*).
6. **API Keys**:
   - **Google AI API Key** (từ [Google AI Studio](https://aistudio.google.com/)).
   - **Pinecone API Key** (từ [Pinecone Dashboard](https://www.pinecone.io/)).
   - **Google Drive OAuth2** (để truy cập file CV).
   - **Gmail OAuth2** (để gửi email báo cáo).
   - **NocoDB API Token** (nếu sử dụng NocoDB).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2987](https://n8n.io/workflows/2987) hoặc copy toàn bộ JSON từ link trên.
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor**.
  - Nhấn **Import** → Dán JSON hoặc tải file JSON.
  - Chọn **Create Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **3 phần chính**:
- **📚 TRAINING (Tự động học tập từ CV)**
- **💬 CHATTING (Chatbot trả lời dựa trên CV)**
- **📊 REPORTING (Gửi báo cáo email hàng ngày)**

##### **A. Cấu Hình Cho Phần TRAINING (Tự động học tập từ CV)**
1. **Google Drive Trigger**
   - **Node 1**: `Google Drive - Resume CV File Created`
     - **Folder ID**: Điền **ID của thư mục Google Drive** bạn đã tạo (để lưu CV).
     - **Mime Types**: Chọn `application/pdf` hoặc `application/vnd.google-apps.document`.
   - **Node 2**: `Google Drive - Resume CV File Updated`
     - **Folder ID**: Cùng với Node 1.
     - **Mime Types**: Cùng với Node 1.

2. **Pinecone Vector Store**
   - **Node**: `Pinecone - Vector Store for CV Content`
     - **Environment**: Chọn môi trường Pinecone của bạn.
     - **Index Name**: Điền `seanrag` (hoặc tên index bạn đã tạo).
     - **API Key**: Điền **Pinecone API Key** từ dashboard Pinecone.

3. **Google Gemini API**
   - **Node**: `Embeddings Google Gemini`
     - **Credentials**: Chọn `googlePalmApi`.
     - **API Key**: Điền **Google AI API Key** từ [Google AI Studio](https://aistudio.google.com/).
   - **Node**: `CV File Data Loader` & `CV content - Recursive Character Text Splitter`
     - **Không cần chỉnh sửa**, workflow sẽ tự động xử lý.

##### **B. Cấu Hình Cho Phần CHATTING (Chatbot trả lời)**
1. **Webhook API (Chatbot)**
   - **Node**: `Chat API - webhook`
     - **Path**: `chat` (không cần đổi).
     - **HTTP Method**: `POST`.
   - **Node**: `Personal CV AI Agent Assistant`
     - **Credentials**: Chọn `googlePalmApi` (đã cấu hình ở phần Training).
   - **Node**: `Resume lookup : Vector Store Tool`
     - **Index Name**: Điền `seanrag` (hoặc tên index của bạn).
   - **Node**: `Resume Embeddings Google Gemini (retrieval)`
     - **Credentials**: Chọn `googlePalmApi`.

2. **Lưu Hội Thoại vào NocoDB**
   - **Node**: `Save Conversation - NocoDB`
     - **Credentials**: Chọn `nocoDbApiToken`.
     - **Table Name**: Điền `ConversationHistory` (hoặc tên bảng của bạn).
     - **Fields**:
       - `user`: Tên người dùng.
       - `email`: Email của người dùng.
       - `ai`: Nội dung trả lời của AI.
       - `sessionid`: ID phiên trò chuyện (có thể tự động sinh).
       - `date`: Ngày hiện tại.
       - `datetime`: Thời gian hiện tại.

3. **Webhook API (Lưu hội thoại từ frontend)**
   - **Node**: `Save Conversation API - Webhook`
     - **Path**: `update-conversation`.
     - **HTTP Method**: `POST`.
   - **Node**: `Save Conversation API Webhook - Response`
     - **Không cần chỉnh sửa**.

##### **C. Cấu Hình Cho Phần REPORTING (Gửi báo cáo email hàng ngày)**
1. **Schedule Trigger**
   - **Node**: `Schedule Trigger`
     - **Cron Expression**: `0 0 * * *` (chạy hàng ngày lúc 00:00).
     - **Time Zone**: Chọn múi giờ của bạn.

2. **Lấy dữ liệu từ NocoDB**
   - **Node**: `NocoDB - get all todays conversation`
     - **Credentials**: Chọn `nocoDbApiToken`.
     - **Table Name**: `ConversationHistory`.
     - **Filter**: `date = today` (để lấy chỉ dữ liệu ngày hôm nay).

3. **Group và Format Email**
   - **Node**: `Group Conversation By Unique Session + Email - Code`
     - **Không cần chỉnh sửa**, workflow sẽ tự động nhóm dữ liệu.
   - **Node**: `Format HTML Display For email`
     - **Không cần chỉnh sửa**, nhưng có thể tùy chỉnh HTML để đẹp hơn.
   - **Node**: `Send Report To Gmail`
     - **Credentials**: Chọn `gmailOAuth2`.
     - **To**: Điền email của bạn hoặc email nhóm.
     - **Subject**: `Báo cáo hội thoại CV ngày [date]`.
     - **Body**: Nội dung HTML đã format.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ liệu Mẫu**
   - **Test Webhook Chat**:
     ```bash
     curl -X POST 'https://n8n.io/webhook-test/chat' -H 'Content-Type: application/json' -d '{"chatInput": "Tôi là ai?"}'
     ```
     - **Kết quả mong đợi**:
       ```json
       [{"output":"Sean là một kỹ sư có kinh nghiệm 15 năm trong ngành..."}]
       ```
   - **Test Webhook Lưu Hội Thoại**:
     ```bash
     curl -X POST 'https://n8n.io/webhook-test/update-conversation' -H 'Content-Type: application/json' -d '{
       "user": "Người dùng mẫu",
       "email": "test@example.com",
       "ai": "AI trả lời mẫu",
       "sessionid": "session123"
     }'
     ```
   - **Test Schedule (Báo cáo Email)**
     - Chờ đến giờ chạy của **Schedule Trigger** (00:00 hàng ngày) hoặc chạy manual.

2. **Bật Active Workflow**
   - Nhấn **Active** trên workflow trong n8n Editor.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**
   - Thay vì gửi email, có thể gửi báo cáo vào **Slack** hoặc **Telegram** bằng node `slack` hoặc `telegramBot`.
   - **Cách làm**:
     - Thêm node `slack` hoặc `telegramBot`.
     - Cấu hình webhook từ Slack/Telegram vào node `respondToWebhook`.

2. **Lưu Log vào Google Sheets**
   - Thay vì NocoDB, có thể lưu dữ liệu vào **Google Sheets** bằng node `googleSheets`.
   - **Lợi ích**: Dễ dàng theo dõi và phân tích dữ liệu.

3. **Tùy Chỉnh Chatbot**
   - **Thêm/Loại bỏ nội dung CV**: Nếu CV có nhiều trang, có thể điều chỉnh **text splitter** để chia nhỏ hơn.
   - **Thay đổi mô hình AI**: Thay **Google Gemini** bằng **OpenAI** (nếu có API key).

4. **Báo cáo Chi Tiết Hơn**
   - Thêm **biểu đồ** vào email bằng **Google Data Studio** hoặc **Power BI**.
   - **Cách làm**:
     - Xuất dữ liệu từ NocoDB/Google Sheets.
     - Kết nối với **Google Data Studio** để tạo báo cáo tự động.

5. **Sử Dụng Frontend Tùy Chỉnh**
   - Nếu muốn xây dựng một **trang web chatbot riêng**, có thể:
     - Sử dụng **React/Vue** kết nối với webhook `chat`.
     - Thay đổi endpoint từ `n8n.io` sang domain riêng (ví dụ: `https://cvbot.example.com/chat`).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa quá trình tương tác với ứng viên thông qua CV. Các sếp sẽ:
✔ **Tiết kiệm thời gian** lên tới **80%** trong việc trả lời câu hỏi về CV.
✔ **Cập nhật tự động** khi CV được chỉnh sửa.
✔ **Lưu trữ và báo cáo** tất cả cuộc trò chuyện một cách chuyên nghiệp.

**Hãy áp dụng ngay và tự động hóa quy trình tuyển dụng của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/2987) và bắt đầu "lên đồ" ngay!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và đánh giá nếu bài hướng dẫn hữu ích!** 🚀