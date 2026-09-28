---
title: "🤖 **Tự Động Hóa OCR + RAG cho Telegram: Bot Asisten Akademik Học Viện ITERA (Gemini + GPT-4 Mini + Supabase)**"
description: "Workflow tự động hóa hoàn chỉnh giúp học viên ITERA quản lý Tugas Akhir (TA) thông minh: OCR tự động từ hình ảnh, trả lời câu hỏi dựa trên RAG từ tài liệu chính thức, và theo dõi status TA 24/7. Giảm thời gian hành chính 90% và loại bỏ sai sót nhân sự."
slug: "bot-asisten-academic-ocr-rag-telegram"
tags: [n8n, automation, ai-chatbot, ocr, rag, telegram-bot, supabase, openai, gemini]
keywords: [n8n workflow telegram bot, tự động hóa quản lý tugas akhir, OCR hình ảnh form học tập, RAG với Supabase, GPT-4 mini cho câu trả lời chính xác, tự động hóa học viện]
---

# 🚀 **Bot Asisten Akademik Học Viện ITERA: OCR + RAG Tự Động Hóa**

## **📌 Nỗi Đau Của Học Viên & Giảng Viên**
Học viên và giảng viên tại Học Viện ITERA thường phải mất **giờ đồng hồ** để:
- **Nhập liệu thủ công** từ hình ảnh form TA (báo cáo, lembar bimbingan, BAP Sempro) → **Tốn thời gian và dễ sai sót**.
- **Tìm kiếm thông tin** về quy trình TA trong tài liệu rải rác → **Không thống nhất, thông tin lỗi thời**.
- **Theo dõi status** của Tugas Akhir → **Không có hệ thống tự động cập nhật**.
- **Trả lời câu hỏi** về quy trình học tập → **Giảng viên phải trả lời nhiều lần cùng một câu hỏi**.

**Workflow này giải quyết tất cả vấn đề trên bằng:**
✅ **OCR tự động** từ hình ảnh → **Không cần nhập liệu thủ công**.
✅ **RAG (Retrieval-Augmented Generation)** với **Supabase Vector Store** → **Trả lời chính xác dựa trên tài liệu chính thức**.
✅ **Theo dõi status TA** từ Google Sheets → **Cập nhật thời gian thực**.
✅ **Lưu lịch sử chat** → **Giúp admin theo dõi và phân tích**.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 90% thời gian** nhập liệu từ hình ảnh form.
- **Giảm sai sót** do nhập liệu thủ công (OCR chính xác với Gemini).
- **Trả lời tự động** cho học viên về quy trình TA (không cần giảng viên phản hồi lặp lại).
- **Cập nhật status TA** tự động từ Google Sheets → **Học viên biết tình trạng Tugas Akhir của mình 24/7**.
- **Lưu lịch sử chat** → **Admin có thể phân tích và cải thiện quy trình**.
- **Hoạt động liên tục** (24/7) → **Không phụ thuộc vào giờ làm việc của nhân viên**.
:::

---

## 🔧 **Yêu Cầu Cần Thiết (Credentials & Hệ Thống)**

### **1. API Keys & Credentials (Bắt Buộc)**
| **Dịch Vụ**               | **API Key/Credential**          | **Lưu Ý**                                                                 |
|---------------------------|---------------------------------|----------------------------------------------------------------------------|
| **Telegram Bot**          | `telegramApi`                   | Bot Telegram để nhận/send tin nhắn. Tạo bot tại [@BotFather](https://t.me/BotFather). |
| **Google Sheets & Drive** | `googleSheetsOAuth2Api`         | Để lưu trữ database TA và tài liệu chính thức.                          |
| **OpenAI**                | `openAiApi`                     | API Key cho **GPT-4.1-mini** và **Embeddings** (dùng cho AI Agent).       |
| **Supabase**              | `supabaseApi`                   | Database vector store cho RAG (tải lên từ Google Drive).                  |
| **Gemini API**            | (Không trong workflow này)      | **Lưu ý:** Workflow sử dụng **HTTP Request** để gọi API Gemini từ bên ngoài. |
| **PostgreSQL**            | `postgres`                      | Để lưu trữ **bộ nhớ chat** (context history).                          |
| **Hugging Face**          | `huggingFaceApi`                | (Nếu muốn thay thế OpenAI Embeddings).                                    |

### **2. Hệ Thống & Dữ liệu Cần Chuẩn Bị**
- **Google Drive** chứa **tài liệu chính thức** (quy trình TA, form mẫu, hướng dẫn).
- **Google Sheets** với tên bảng:
  - `TA_SEMPRO_DATABASE` (để lưu trữ dữ liệu OCR từ hình ảnh).
  - `CHAT_HISTORY` (nếu muốn lưu lịch sử chat).
- **Supabase Project** đã cấu hình **Vector Store** (table `documents`).
- **Telegram Channel/Group** để bot hoạt động.

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/15564](https://n8n.io/workflows/15564).
2. **Nhấn "Import"** trong n8n Editor hoặc **copy JSON** và dán vào **Import Workflow** (tùy chọn).
3. **Chọn "Self-hosted"** nếu bạn đang chạy n8n trên VPS.

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **2. Cấu Hình Cần Thiết (Bắt Buộc)**

#### **A. Cấu Hình Credentials**
| **Node**               | **Cần Thiết** | **Cách Cấu Hình**                                                                 |
|------------------------|---------------|----------------------------------------------------------------------------------|
| **Telegram Trigger**   | ✅            | Chọn `telegramApi` đã tạo trước.                                                 |
| **Telegram (Send/Respon)** | ✅       | Chọn `telegramApi` cùng một credential.                                           |
| **Google Sheets**      | ✅            | Chọn `googleSheetsOAuth2Api` và chọn sheet `TA_SEMPRO_DATABASE`.                 |
| **OpenAI (GPT-4 Mini)** | ✅          | Chọn `openAiApi` và chọn model `gpt-4.1-mini`.                                      |
| **Supabase**           | ✅            | Chọn `supabaseApi` và chọn table `documents` trong Vector Store.                  |
| **PostgreSQL**         | ✅            | Chọn `postgres` và cấu hình connection string.                                   |
| **Google Drive Trigger** | ✅         | Chọn `googleDriveOAuth2Api` và cấu hình folder chứa tài liệu chính thức.         |

#### **B. Cấu Hình Node Quan Trọng**
1. **`Analisa gambar` (HTTP Request)**
   - **URL:** `https://generativeai.googleapis.com/v1beta/models/gemini-pro:generateContent`
   - **Headers:** `Authorization: Bearer {API_KEY_GEMINI}`
   - **Body (JSON):**
     ```json
     {
       "contents": [{"parts": [{"inline_data": {"mime_type": "image/jpeg", "data": "{{$json.base64Image}}"}}}]}]
     }
     ```
   - **Lưu ý:** Nếu không có API Gemini, có thể thay thế bằng **OCR từ Tesseract** (node `extractFromFile`).

2. **`AI Agent` (GPT-4o mini)**
   - **Model:** `gpt-4o-mini` (đã cấu hình trong `keyParameters`).
   - **Prompt:** Cần **tùy chỉnh** để phù hợp với quy trình TA của ITERA.
     Ví dụ:
     ```plaintext
     Bạn là trợ lý quản lý Tugas Akhir của Học Viện ITERA. Trả lời dựa trên:
     1. Tài liệu chính thức trong Supabase Vector Store.
     2. Dữ liệu từ Google Sheets (TA_SEMPRO_DATABASE).
     Nếu không biết, hãy trả lời: "Xin lỗi, tôi không có thông tin về điều đó. Vui lòng liên hệ admin."
     ```

3. **`Supabase Vector Store`**
   - **Table:** `documents` (đã tạo trước).
   - **Collection:** `rag_collection` (nếu có).
   - **Lưu ý:** Nếu chưa có, **tải tài liệu từ Google Drive** vào Supabase trước.

4. **`Google Sheets Tool` (Lấy dữ liệu)**
   - **Range:** `TA_SEMPRO_DATABASE!A1:Z1000` (điều chỉnh theo số lượng dữ liệu).
   - **Query:** `SELECT * WHERE "Status" = "Pending"` (ví dụ).

5. **`ExecuteWorkflowTrigger` (Nếu cần gọi workflow khác)**
   - **Workflow:** Chọn workflow khác để xử lý thêm (ví dụ: gửi email admin).

---

### **3. Kích Hoạt Workflow**
1. **Test Run với Dữ liệu Mẫu**
   - Gửi **/help** trên Telegram để kiểm tra bot trả lời chính xác.
   - Upload **hình ảnh form TA** để kiểm tra OCR.
   - Gửi **câu hỏi về quy trình TA** để kiểm tra RAG.

2. **Bật Active Workflow**
   - Nhấn **Active** trên n8n Editor.
   - **Monitor Logs** để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa OCR**
- **Nếu Gemini API đắt**, thay thế bằng:
  ```plaintext
  - Node `extractFromFile` (binaryToProperty) + Tesseract OCR (n8n-node-tesseract).
  - Hoặc sử dụng **EasyOCR** (node `@n8n/n8n-nodes-easyocr`).
- **Cải thiện chất lượng hình ảnh** trước khi OCR:
  - Sử dụng node `imageProcessing` (n8n-node-image-processing) để tăng độ nét.

### **2. Cải Tiến RAG**
- **Tăng độ chính xác** bằng cách:
  - **Chunking tài liệu** nhỏ hơn (ví dụ: 500 từ/chunk).
  - **Sử dụng embeddings Hugging Face** thay vì OpenAI (rẻ hơn).
  - **Lọc kết quả** trước khi trả lời (ví dụ: chỉ trả lời từ tài liệu mới nhất).

### **3. Theo Dõi & Log**
- **Lưu lịch sử chat** vào Google Sheets:
  ```plaintext
  - Node `googleSheets` (appendOrUpdate) với sheet `CHAT_HISTORY`.
  - Cấu hình cột: `user_id`, `message`, `timestamp`, `response`.
- **Gửi báo cáo định kỳ** (ví dụ: hàng tuần):
  - Sử dụng node `executeWorkflowTrigger` để gọi workflow báo cáo.

### **4. Kết Nối với Slack/Email**
- **Gửi thông báo lỗi** đến Slack/Email:
  ```plaintext
  - Node `webhook` (Slack) hoặc `email` (n8n-node-email).
  - Khi OCR thất bại, bot gửi cảnh báo: "Hình ảnh không rõ, vui lòng tải lại."
- **Gửi thông báo status TA** cho học viên:
  ```plaintext
  - Node `telegram` với tin nhắn tự động: "Status Tugas Akhir của bạn: {{status}}."
  ```

### **5. Cập Nhật Tài Liệu RAG**
- **Tự động tải mới tài liệu** từ Google Drive:
  ```plaintext
  - Sử dụng `googleDriveTrigger` để kích hoạt khi có file mới.
  - Node `documentDefaultDataLoader` + `vectorStoreSupabase` để cập nhật vector store.
  ```

---

## 📌 **Kết Luận: Áp Dụng Ngay Hôm Nay!**

Workflow này **giải phóng thời gian** cho giảng viên và học viên, đồng thời **giảm sai sót** trong quản lý Tugas Akhir. Với **OCR tự động, RAG chính xác, và theo dõi status 24/7**, Học Viện ITERA có thể **tăng cường hiệu quả hành chính** mà không cần viết code.

### **Bước Tiếp Theo**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Cấu hình tất cả credentials** (Telegram, Google, OpenAI, Supabase).
3. **Import workflow** và **test với dữ liệu mẫu**.
4. **Tùy chỉnh prompt AI Agent** phù hợp với quy trình TA của ITERA.
5. **Bật Active** và **monitor logs** để đảm bảo hoạt động ổn định.

**🚀 Hãy tự động hóa quản lý Tugas Akhir của bạn ngay hôm nay!** Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ admin n8n cho hỗ trợ.

---
**📌 Chú ý:** Workflow này **không sử dụng Gemini API trực tiếp**, mà gọi API từ bên ngoài (HTTP Request). Nếu muốn sử dụng Gemini, cần **cấu hình thêm node HTTP Request** với API Key Gemini.