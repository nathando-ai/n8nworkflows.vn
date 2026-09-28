---
title: "🤖 **Hệ Thống RAG Doanh Nghiệp Tự Động Với Google Gemini: Tìm Kiếm File + Trả Lời AI Voice (N8N)**"
description: "Tự động hóa hệ thống RAG (Retrieval-Augmented Generation) doanh nghiệp với Google Gemini, cho phép tìm kiếm nội dung từ Google Drive, lưu trữ trên Google Sheets và trả lời tự động bằng giọng AI. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin và cải thiện trải nghiệm khách hàng/nhân viên."
slug: "huong-dan-rag-google-gemini-n8n"
tags: [n8n, automation, ai-rag, google-gemini, google-drive, google-sheets, no-code]
keywords: [n8n workflow rag, tự động hóa tìm kiếm file, google gemini n8n, hệ thống tra cứu doanh nghiệp, ai voice response]
---

# 🚀 **Hệ Thống RAG Doanh Nghiệp Tự Động Với Google Gemini: Tìm Kiếm File + Trả Lời AI Voice**

### **Giải pháp cho vấn đề gì?**
Các sếp đã từng gặp phải tình trạng này chưa?
- **Tốn thời gian** tìm kiếm thông tin trong hàng trăm file Google Drive để trả lời câu hỏi của khách hàng/nhân viên.
- **Không chính xác** khi nhớ lại nội dung từ nhiều tài liệu.
- **Không cá nhân hóa** trong tương tác với khách hàng.
- **Không hoạt động 24/7**, phải phụ thuộc vào nhân viên trực ca.

**Workflow này giúp giải quyết tất cả!** Nó tự động hóa việc **tìm kiếm nội dung từ Google Drive**, **lưu trữ trên Google Sheets**, và **trả lời tự động bằng giọng AI** (Google Gemini) khi có câu hỏi. Dễ dàng tích hợp vào hệ thống nội bộ hoặc hỗ trợ khách hàng qua chatbot.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tìm kiếm siêu tốc**: AI tìm kiếm nội dung chính xác trong Google Drive chỉ trong giây lát.
✅ **Trả lời tự động bằng giọng AI**: Khách hàng/nhân viên nhận câu trả lời **như người thật** (Google Gemini).
✅ **Lưu trữ thông minh**: Tất cả dữ liệu được **cập nhật tự động** trên Google Sheets.
✅ **Hoạt động 24/7**: Không cần nhân viên trực ca, hệ thống **chạy liên tục**.
✅ **Tích hợp dễ dàng**: Hoàn toàn **không cần code**, chỉ cần cấu hình n8n.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (Google Drive + Google Sheets) với quyền **quản trị viên**.
✔ **API Key của Google Gemini** (mua trên [Google AI Store](https://ai.google.com/)).
✔ **Tài khoản n8n** (self-hosted hoặc n8n.cloud).
✔ **File PDF/PPTX/DOCX** trong Google Drive để **tạo kho dữ liệu RAG**.
✔ **Webhook URL** (nếu muốn kết nối với Slack/Telegram/email).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11269](https://n8n.io/workflows/11269).
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn workspace** (nếu self-hosted) và nhấn **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
2. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/11269](https://n8n.io/workflows/11269) → Dán vào.
3. **Nhấn "Import"** và chọn workspace.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node**, nhưng các sếp cần chú ý **các node quan trọng sau**:

#### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần chỉnh gì**, chỉ dùng để **test workflow** trước khi kích hoạt tự động.

#### **🔹 Node 2-5: Tạo & Lưu Trữ Dữ liệu RAG (Google Drive → Google Sheets)**
1. **"Google Drive - RAG Source" (googleDriveTrigger)**
   - **Chọn folder** trong Google Drive chứa file cần **tạo kho dữ liệu**.
   - **Cài đặt**: Chọn **"File change"** (để theo dõi thay đổi file mới).

2. **"Download file" (googleDrive)**
   - **Không cần chỉnh**, node này tự động **tải file** từ Google Drive.

3. **"Store File Store" (googleSheets)**
   - **Chọn Sheet** trong Google Sheets để **lưu metadata** của file (tên, đường dẫn, loại file).
   - **Cấu hình**:
     - **Sheet Name**: `RAG_File_Store` (hoặc tên tùy chỉnh).
     - **Range**: `A1` (để ghi dữ liệu từ ô A1).
     - **Credentials**: Chọn tài khoản Google đã kết nối với n8n.

#### **🔹 Node 6-9: Tải File lên Google Gemini Search**
1. **"Create Gemini File Search Store" (httpRequest)**
   - **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=YOUR_API_KEY`
   - **Headers**:
     - `Content-Type: application/json`
   - **Body (JSON)**:
     ```json
     {
       "contents": [
         {
           "parts": [
             {"text": "Tạo kho tìm kiếm cho file: ${{ $json["fileName"] }}"}
           ]
         }
       ]
     }
     ```
   - **Thay thế `YOUR_API_KEY`** bằng API Key của Google Gemini.

2. **"Upload the Actual File" (httpRequest)**
   - **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:uploadFile?key=YOUR_API_KEY`
   - **Headers**:
     - `Content-Type: multipart/form-data`
   - **Body (File Upload)**:
     - **Chọn file** từ node **"Download file"** (node 4).
     - **Tham số**: `file` (tên field mặc định).

#### **🔹 Node 10-15: Chat AI + Trả Lời Tự Động**
1. **"When chat message received" (chatTrigger)**
   - **Không cần chỉnh**, node này **chờ nhận câu hỏi** từ người dùng.

2. **"Google Gemini Chat Model" (lmChatGoogleGemini)**
   - **Model**: Chọn `gemini-pro`.
   - **API Key**: Điền **API Key Google Gemini**.
   - **Prompt**: Cấu hình như sau:
     ```plaintext
     Bạn là một trợ lý AI chuyên nghiệp. Trước khi trả lời, hãy tìm kiếm thông tin từ kho dữ liệu RAG (Google Drive) để đảm bảo câu trả lời chính xác.
     Nếu không tìm thấy thông tin, hãy nói: "Tôi không tìm thấy thông tin này. Bạn có thể kiểm tra lại hoặc liên hệ quản trị viên."
     ```

3. **"Search Tool" (httpRequestTool)**
   - **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:search?key=YOUR_API_KEY`
   - **Headers**:
     - `Content-Type: application/json`
   - **Body (JSON)**:
     ```json
     {
       "contents": [
         {
           "parts": [
             {"text": "${{ $json["question"] }}"}
           ]
         }
       ],
       "searchConfig": {
         "fileSearchConfig": {
           "fileSearchStoreId": "${{ $json["fileSearchStoreId"] }}"
         }
       }
     }
     ```

4. **"AI Powered RAG Agent" (agent)**
   - **Cấu hình agent**:
     - **Model**: `Google Gemini`.
     - **Tools**: Chọn **"Search Tool"** (node 11).
     - **Prompt**: Cấu hình như sau:
       ```plaintext
       Bạn là một agent RAG. Khi nhận câu hỏi, hãy:
       1. Tìm kiếm thông tin từ kho dữ liệu RAG.
       2. Nếu tìm thấy, trả lời dựa trên dữ liệu đó.
       3. Nếu không tìm thấy, hãy nói: "Tôi không có thông tin này."
       ```

5. **"Webhook" & "Respond to Webhook" (webhook + respondToWebhook)**
   - **Cấu hình Webhook**:
     - **URL**: Nhập **URL Webhook** của Slack/Telegram/email (nếu muốn tích hợp).
     - **Method**: `POST`.
   - **Cấu hình "Respond to Webhook"**:
     - **Trả lời tự động** với giọng AI (nếu kết nối với Slack/Telegram).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute workflow"** (node 1) → Kiểm tra **Google Sheets** có cập nhật metadata không.
   - Gửi **câu hỏi test** vào Webhook (nếu có) → Kiểm tra AI trả lời có chính xác không.

2. **Bật Active workflow**:
   - Nhấn **"Active"** trên tab **Workflow** trong n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Telegram**
- **Cấu hình Webhook** trong Slack/Telegram để **nhận câu hỏi tự động**.
- **Cài đặt bot** trả lời bằng giọng AI (sử dụng **node `respondToWebhook`**).

### **2. Lưu log hoạt động**
- **Thêm node `set`** sau **"AI Powered RAG Agent"** để **lưu log** vào Google Sheets:
  ```json
  {
    "json": {
      "timestamp": "${{ $datetime('YYYY-MM-DD HH:mm:ss') }}",
      "question": "${{ $json['question'] }}",
      "answer": "${{ $json['answer'] }}"
    }
  }
  ```

### **3. Gửi báo cáo định kỳ**
- **Sử dụng node `set` + `googleSheets`** để **tạo báo cáo** về số lượng câu hỏi, thời gian phản hồi.
- **Kết hợp với node `email`** để gửi báo cáo hàng tuần cho quản lý.

### **4. Cập nhật kho dữ liệu tự động**
- **Sử dụng `googleDriveTrigger`** để **theo dõi thay đổi file mới** trong Google Drive.
- **Cấu hình `cron`** (nếu self-hosted) để **tải file mới vào Gemini** mỗi ngày.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách **tự động hóa tìm kiếm và trả lời AI** từ Google Drive. Không cần **code**, chỉ cần **cấu hình n8n** và tích hợp với Google Gemini.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/11269](https://n8n.io/workflows/11269).
2. **Cấu hình Google Drive, Sheets và API Key**.
3. **Test và kích hoạt** để **tận hưởng hiệu quả ngay**.

🚀 **N8N + Google Gemini = Hệ thống RAG Doanh Nghiệp Siêu Tốc!** 🚀

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để **self-host** và chạy workflow **ổn định 24/7**!