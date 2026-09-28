---
title: "🚀 Tự Động Hoàn Thành Vector Store Cá Nhân Từ Google Sheets Với OpenAI & Gemini AI (Không Cần Code)"
description: "Workflow này tự động chuyển đổi dữ liệu cá nhân từ Google Sheets thành vector store thông minh, cho phép AI (OpenAI/Gemini) trả lời nhanh chóng và chính xác mọi câu hỏi liên quan. Giúp tiết kiệm thời gian lên tới 80% trong việc quản lý và truy vấn dữ liệu cá nhân."
slug: "tieu-dong-hoan-thanh-vector-store-google-sheets-openai-gemini"
tags: [n8n, automation, no-code, ai-multimodal, vector-database, google-sheets, openai, gemini-ai, supabase]
keywords: [n8n workflow tự động hóa, vector store cá nhân, google sheets + ai, tự động hóa dữ liệu cá nhân, gemini ai + openai, supabase vector database]
---

# 🚀 **Tự Động Hoàn Thành Vector Store Cá Nhân Từ Google Sheets Với OpenAI & Gemini AI**

### **Giải Pháp Cho Người Dùng Tự Động Hóa Quản Lý Dữ Liệu Cá Nhân**
Bạn đã bao giờ phải mất nhiều giờ để tìm kiếm thông tin cá nhân trong các tệp Excel, email hay Google Sheets? Hay phải nhớ hàng loạt mật khẩu, địa chỉ liên lạc, lịch sử mua sắm? **Workflow này sẽ tự động hóa toàn bộ quá trình**, biến dữ liệu của bạn thành một **vector store thông minh**, cho phép AI (OpenAI và Gemini) trả lời mọi câu hỏi chỉ bằng một câu lệnh.

Với **n8n**, bạn không cần viết một dòng code nào cả. Chỉ cần kết nối Google Sheets với AI, và hệ thống sẽ tự động:
✅ **Chuyển đổi dữ liệu thành vector** (OpenAI Embeddings)
✅ **Lưu trữ trên Supabase** (vector database hiệu suất cao)
✅ **Cho phép AI trả lời nhanh chóng** (Gemini hoặc OpenAI Chat)
✅ **Giữ nhớ lịch sử trò chuyện** (PostgreSQL Memory)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** khi tìm kiếm thông tin cá nhân (không cần mở tệp Excel).
- **Trả lời tức thì** mọi câu hỏi về dữ liệu cá nhân (ví dụ: *"Hãy cho tôi biết lịch sử mua sắm của tôi trong tháng 12/2023"*).
- **Cá nhân hóa hoàn toàn** – AI hiểu ngữ cảnh và nhớ lịch sử trò chuyện.
- **Hoạt động liên tục 24/7** – Dữ liệu luôn được cập nhật và sẵn sàng truy vấn.
- **Bảo mật cao** – Dữ liệu được lưu trên Supabase (có thể cấu hình quyền truy cập).
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để đọc dữ liệu cá nhân).
✔ **API Key OpenAI** (để tạo embeddings).
✔ **API Key Google Gemini** (để sử dụng AI trả lời).
✔ **Tài khoản Supabase** (để lưu vector store).
✔ **Tài khoản PostgreSQL** (để lưu nhớ lịch sử trò chuyện).
✔ **Workflow n8n** (cài đặt trên máy chủ hoặc VPS).

---
:::note[CHÚ Ý]
- **Dữ liệu trong Google Sheets phải được cấu trúc rõ ràng** (mỗi hàng là một bản ghi cá nhân).
- **Supabase và PostgreSQL phải được cấu hình sẵn** trước khi import workflow.
- **API Key phải được lưu trữ an toàn** trong n8n (không chia sẻ công khai).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/7299](https://n8n.io/workflows/7299) (chọn **Export JSON**).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor và tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ mã JSON từ workflow gốc.
3. Chọn **Create new workflow**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **11 node** quan trọng, mỗi node cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: "When chat message received" (chatTrigger)**
- **Chức năng**: Khởi động workflow khi nhận được tin nhắn (ví dụ: từ Slack, Telegram hoặc webhook).
- **Cấu hình**:
  - Chọn **Trigger Type**: `Webhook` (nếu muốn gọi thủ công) hoặc `Slack/Telegram` (nếu muốn tích hợp).
  - **Path**: Đặt tên duy nhất (ví dụ: `/chat-personal-data`).

#### **🔹 Node 2: "Get row(s) in sheet1" (googleSheets)**
- **Chức năng**: Đọc dữ liệu từ Google Sheets.
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (cần thiết lập OAuth2 trước).
  - **Sheet Name**: Đặt tên sheet chứa dữ liệu cá nhân (ví dụ: `personal_data`).
  - **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A1:Z1000`).

#### **🔹 Node 3: "Convert to File" (convertToFile)**
- **Chức năng**: Chuyển dữ liệu từ Google Sheets thành định dạng file (JSON).
- **Cấu hình**:
  - **File Type**: Chọn `JSON`.
  - **Data**: Chọn output từ node `Get row(s) in sheet1`.

#### **🔹 Node 4: "Embeddings OpenAI" (embeddingsOpenAi)**
- **Chức năng**: Tạo embeddings cho dữ liệu bằng OpenAI.
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `text-embedding-ada-002` (mặc định).
  - **Input**: Chọn output từ node `Convert to File`.

#### **🔹 Node 5: "Supabase Vector Store" (vectorStoreSupabase)**
- **Chức năng**: Lưu embeddings vào Supabase.
- **Cấu hình**:
  - **Credentials**: Chọn `supabaseApi`.
  - **Table Name**: Đặt tên bảng (ví dụ: `personal_data_vectors`).
  - **Vector Dimension**: Đặt theo model embeddings (ví dụ: `1536` cho `text-embedding-ada-002`).

#### **🔹 Node 6: "Postgres Chat Memory" (memoryPostgresChat)**
- **Chức năng**: Lưu lịch sử trò chuyện vào PostgreSQL.
- **Cấu hình**:
  - **Credentials**: Chọn `postgres`.
  - **Table Name**: Đặt tên bảng (ví dụ: `chat_history`).
  - **Columns**: Thêm cột `user_id`, `message`, `timestamp`.

#### **🔹 Node 7: "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Chức năng**: Sử dụng Gemini AI trả lời câu hỏi.
- **Cấu hình**:
  - **Credentials**: Chọn `googlePalmApi`.
  - **Model**: Chọn `gemini-pro`.
  - **Prompt**: Cấu hình template để AI hiểu ngữ cảnh (ví dụ:
    ```
    You are a personal assistant. Answer questions based on the user's personal data stored in Supabase vector store.
    If you don't know the answer, say "I don't have that information in my records."
    ```).

#### **🔹 Node 8: "AI Agent" (agent)**
- **Chức năng**: Quản lý logic AI (tìm kiếm vector store và trả lời).
- **Cấu hình**:
  - **Agent Type**: Chọn `LangChain Agent`.
  - **Tools**: Kết nối với `Supabase Vector Store` và `Postgres Chat Memory`.
  - **Prompt**: Cấu hình để AI sử dụng vector store và nhớ lịch sử:
    ```
    Use the vector store to find relevant personal data. If the user asks about past conversations, refer to the chat memory.
    ```).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một tin nhắn mẫu (ví dụ: *"Hãy cho tôi biết địa chỉ email của tôi trong tháng 11/2023"*).
   - Kiểm tra AI trả lời chính xác hay không.
2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.
   - Kiểm tra log để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để AI trả lời trên kênh chat.
   - **Cách làm**:
     - Thêm node `Slack/Telegram` sau `chatTrigger`.
     - Cấu hình webhook từ Slack/Telegram vào `chatTrigger`.

2. **Lưu Log Trò Chuyện**:
   - Sử dụng node `n8n-nodes-base.email` để gửi báo cáo hàng tuần về lịch sử truy vấn.
   - **Cách làm**:
     - Thêm node `Email` sau `Postgres Chat Memory`.
     - Cấu hình gửi email định kỳ bằng `n8n-nodes-base.cron`.

3. **Cập Nhật Dữ Liệu Tự Động**:
   - Sử dụng `n8n-nodes-base.cron` để tự động cập nhật dữ liệu từ Google Sheets mỗi ngày.
   - **Cách làm**:
     - Thêm node `Cron` trước `Get row(s) in sheet1`.
     - Đặt lịch chạy (ví dụ: `0 0 * * *` – mỗi ngày 00:00).

4. **Bảo Mật Dữ Liệu**:
   - **Mask sensitive data** trong Google Sheets (ví dụ: số điện thoại, CMND).
   - **Sử dụng Supabase Row-Level Security (RLS)** để chỉ cho phép truy cập dữ liệu cá nhân của người dùng.

---

## 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi việc tìm kiếm dữ liệu thủ công**, thay vào đó là một **AI cá nhân hóa** trả lời mọi câu hỏi chỉ bằng một câu lệnh. **Không cần code, không cần kỹ thuật cao** – chỉ cần kết nối các dịch vụ và chạy!

👉 **Bắt đầu ngay hôm nay**:
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình các API Key** và credentials.
3. **Test với dữ liệu mẫu** và bật workflow.
4. **Tích hợp vào Slack/Telegram** để sử dụng dễ dàng hơn.

**Nếu bạn gặp khó khăn trong quá trình setup, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).** 🚀

---
**#TựĐộngHóa #AIMultimodal #N8nWorkflow #VectorDatabase #GoogleSheets**